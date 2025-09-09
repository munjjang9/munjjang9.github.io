---
layout: post
title: 윈도우 메시지 처리
author: munjjang9
tags: [Windows]
date: 2024-12-16 18:00 +0900
categories: [Study]
toc: true
---

## WndProc

우리가 윈도우에서 어떤 프로그램을 실행시키면 그 프로그램은 윈도우라는 운영체제 위에서 동작하게 된다. 그럼 만약 그 프로그램에서 우리가 어떤 동작을 하게 되면, 그 동작은 어떻게 처리될까?

Direct X를 가지고 프로그래밍을 하려고 하는데, 이를 렌더링 해줄 창이 필요하다. 따라서 윈도우 상에 창을 하나 띄워, 이 창에 동작을 넘겨보도록 하려고 한다.

기본적인 구조로는 윈도우 창을 하나 생성하고, 실행을 한다.

<br>

---

WNDCLASSEX라는 구조체를 통해 윈도우 창을 생성해보려 한다.

### 생성

```c
WNDCLASSEX wndClass;

wndClass.cbSize = sizeof(WNDCLASSEX); 

wndClass.style = CS_HREDRAW | CS_VREDRAW;

wndClass.lpfnWndProc = WndProc;

wndClass.cbClsExtra = 0;

wndClass.cbWndExtra = 0;

wndClass.hInstance = HInstance;

wndClass.hIcon = LoadIcon(nullptr, IDI_APPLICATION);

wndClass.hIconSm = LoadIcon(nullptr, IDI_APPLICATION);

wndClass.hCursor = LoadCursor(nullptr, IDC_ARROW);

wndClass.hbrBackground = (HBRUSH)(COLOR_WINDOW + 2);

wndClass.lpszMenuName = nullptr;

wndClass.lpszClassName = ClassName;
```

- cbSize : 구조체의 크기를 설정

- style : 창이 생성될 스타일을 설정. 위의 경우, 가로와 세로 길이만 설정

- lpfnWndProc : 창 프로시저에 대한 롱 포인터

- cbClsExtra : 창 클래스 구조 다음에 할당해 줄 추가 바이트

- cbWndExtra : 창 인스턴스 다음에 할당할 추가 바이트

- hInstance : 클래스의 창 프로시저가 포함된 인스턴스에 대한 핸들

- hIcon : 윈도우 하단 바에 표시되는 아이콘. 클래스 아이콘에 대한 핸들

- hIconSm : 창 좌측 상단에 표시되는 아이콘

- hCursor : 클래스 커서에 대한 핸들. 커서의 모양

- hbrBackground : 클래스 배경 브러시에 대한 핸들. 배경을 그릴 때 사용하는 브러시

- lpszMenuName : 리소스 파일에 이름이 표시될 때 클래스 메뉴의 리소스 이름을 지정하는 null로 끝나는 문자열에 대한 포인터

- lpszClassName : null로 끝나는 문자열에 대한 포인터 혹은 원자. 문자열일 경우, 창 좌측 상단에 표시되는 창의 이름

<br>

이런 항목들을 구성하여 창을 생성하기 위한 구조체를 형성한다. 그 다음에 윈도우 핸들을 생성하여 파라미터들을 전달해주고, ShowWindow() 함수를 통해 윈도우를 표출한다.

SetForegroundWindow() 함수를 통해 윈도우를 가장 앞에 배치해주고, SetFocus() 함수를 통해 키보드 포커스를 지정해준다.

<br>

---

그 다음엔 생성한 창을 실행해보자. 여기서 실행이란, 윈도우 창 내에서의 동작을 감지하고 이에 대한 처리를 뜻한다.

### 실행

```c
MSG msg;
ZeroMemory(&msg, sizeof(MSG));

while(true)
{
    if(PeekMessage(&msg, nullptr, 0, 0, PM_REMOVE))
    {
        if(msg.message == WM_QUIT)
            break;

        TranslateMessage(&msg);
        DispatchMessage(&msg);
    }
    else
    {
        ~
    }

    return msg.wParam;
}
```

위는 윈도우 창에서의 실행을 코드로 나타낸 것이다.

일단 메시지를 담고 있는 msg 구조체를 ZeroMemory 함수를 통해 초기화를 해준다.

그리고 PeekMessage 함수를 통해 메시지 큐에 담긴 메시지를 꺼내온다. 만약 끝내라는 명령을 가진 메시지가 전달된다면 break가 걸리게 된다. WM_QUIT은 Alt+F4나 닫기 버튼이 이에 해당한다.

TranslateMessage는 키보드나 마우스의 입력을 메시지 형태로 전환하는 역할을 한다.

DispatchMessage는 큐에서 꺼내온 메시지를 WndProc이라는 메시지 처리를 담당하는 함수에게로 전달한다.

<br>

---

마지막으로 메시지를 처리하는 WndProc 함수에 대해 알아보자

### 메시지 처리

```c
LRESULT CALLBACK WndProc(HWND Handle, UINT Message, WPARAM WParam, LPARAM LParam)
{
    switch(Message)
    {
        case WM_KEYDOWN:
        {
            if(WParam == VK_ESCAPE)
            {
                PostQuitMessage(0);

                return 0;
            }

            if(WParam == 0x41)
            {
                MessageBox(nullptr, L"A 눌림", L"A Pressed", MB_OK);

                return 0;
            }
        }

        case WM_DESTROY:
        {
            PostQuitMessage(0);

            return 0;
        }
    }
}
```

위 코드를 보았을 때, WParam 인자를 통해 ESC 키에 대한 메시지가 전달되면, PostQuitMessage(0)가 전달된다. PostQuitMessage(0)은 창에 대한 종료를 호출하고, 창이 종료되게 된다.

WParam == 0x41은 키보드의 'A'키가 눌렸을 때를 의미한다. 이 때, 메시지 박스가 나타나고, 메시지 박스 좌측 상단에는 'A Pressed'가, 메시지 박스 내부에는 'A 눌림'이 나타난다. MB_OK는 확인 버튼이 나타나게 한다.

마지막으로 WM_DESTROY는 WM_QUIT이 받아오는 Alt+F4나 창 닫기 버튼에 대한 처리를 담당한다.

만약, PostQuitMessage(0)가 콜 되지 않았을 경우, 백그라운드 프로세스로서 남아 동작하며, 프로세스가 완전히 종료되지 않는다.

<br>
<br>
<br>
<br>

- 참조 : https://learn.microsoft.com/ko-kr/windows/win32/api/winuser/ns-winuser-wndclassexa