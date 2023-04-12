프로그래밍 언어 : [[C++]]

---
<details>
    <summary>파일 이름 정할 시 앞의 접두사 정리</summary>
	<ul>
		<li> 핸들 :  H</li>
		<li> 클래스 :  C</li>	
		<li> 멤버변수 :  m_</li>
		<li> 메시지 :  WM</li>
</ul>
</details>

---
# 개요

- 운영체제는 3가지 [동적 연결 라이브러리](https://www.notion.so/94b78ef4a5da455caad3f39be00f2fb7) (DLL)로 구성됨 (1)kernel 2) User 3)GDL)
- 특징 : 1️⃣ 장치독립적 2️⃣ 멀티태스킹 지원 3️⃣ 메시지 구동방식 4️⃣ GUI 인터페이스
- 개발 GDI 라이브러리 : WinAPI(기본 API, 다른 라이브러리도 결국 winAPI를 이용하여 개발하는 방식), MFC , WTL .NET
- 개발 방법(자세한 건 잘 모르겠어)

|      | API | MFC | RAD | SDK(소프트웨어 개발키트) |
| ---- | --- | --- | --- | ------------------------ |
| 정의 |   운영체제가 응용 프로그램을 위해 제공하는 함수의 집합 | 가장 많이 사용되는 방법    |  DB 애플리케이션 등에는 적합응용 프로그램 작성에는 부적합   |   |
| 장점 |  • low 레벨의 프로그래밍이 가능   |  • API함수들과 함께 사용가능   |  • 프로그램의 개발이 비교적 쉽다   |                          |
|      |  • 윈도우의 동작 원리 이해   | • RAD툴과 같은 비주얼 기능 제공    |   • 배우기 쉽고 구현하기 쉽다  |                          |
|      |  • 우수한 성능   |• 컴포넌트 프로그래밍에 적합    | • 컴포넌트 환경에 적합    |                          |
| 단점 |     |  • 배우기 어렵다   |  • 빨리 APP 개발 ⭕   |                          |
|      |     |  • 요즘 잘 쓰지도 않는다   |  • low 레벨을 다루지 않아, 메모리 관리가 어렵다   |                          |
|  예시    |   WinAPI  |     |     |        JAVA SDK                  |

- API : 소프트웨어 프로그램이 서로 상호 작용할 수 있도록하는 인터페이스 
- SDK : 특정 플랫폼을 대상으로하는 소프트웨어 응용 프로그램을 개발하는 데 사용할 수있는 도구 집합

# WinAPI
- 윈도우에서 제공하는 기본 API (C언어 기반)
- 윈도우에서 실행되는 라이브러리는 내부적으로 전부 WinAPI를 호출하는 형식을 갖춤
## 1. 이론
- **클래스와 윈도우 클래스의 차이**
        1. 클래스 : tyde
        2. 윈도우 클래스 : 구조체, 종류, 등급 등

- **전반적인 흐름**
        이벤트 발생 → 메시지 → 시스템 프로그램 큐 → 응용 프로그램 큐 → WinMain(메시지 루프) → 운영체제 → WndProc(실질적인 메시지 처리) → 디폴트 WndProc 
        
- **헤더파일** :`#include <windows.h>`
        
- **WinMain** : 1️⃣정의 2️⃣등록(Register) 3️⃣생성(Create) 4️⃣Show 5️⃣메시지 루프(Message roop)
    윈도우 메인 함수로 콘솔에서의 main()에 해당, 프로그램의 진입점(Entry Point)
    1. 정의 : 인스턴스를 통해 생성된 구조체를 사용해서 총 10개의 속성을 정의
    2. 등록(Register) : 정의 후 밑에 쓰는 것이 일반적인듯?
        `if (!RegisterClass(&WndClass)) return NULL; //윈도우 클래스 등록`
    3. 생성(Create) : 생성한 핸들 변수를 이용해 정의(`hWnd = CreateWindow()`)
        1️⃣선언한 클래스 이름 2️⃣ 타이틀 3️⃣ 윈도우 스타일 4️⃣x, y 좌표 5️⃣윈도우 크기 6️⃣(HWND)부모 윈도우 7️⃣(HMENU)메뉴핸들 or 차일드 윈도우 ID 8️⃣인스턴스 핸들 9️⃣여분 데이터(CREATESTRUCT라는 구조체의 번지, 특수한 목적에 사용됨)
    4. Show `ShowWindow(hWnd, nCmdShow);`
        WS_VISIBLE(윈도우 스타일) = show
    5. 메시지 루프(Message roop)
        프로그램이 종료될 때까지 계속 반복
        ```cpp
            while (GetMessage(&msg, NULL, 0, 0))
            {
                TranslateMessage(&msg);
                DispatchMessage(&msg);
            }
        ```
        1. GetMessage(&msg, NULL, 0, 0)
	        - 메시지 큐에서 메시지를 읽어들이고 첫 번째 매개변수가 지정하는 MSG 구조체)에 저장됨.
	        - 이 함수는 읽어들인 메시지가 WM_OUIT이 아닌이상 True만 리턴
	        - 나머지 3개의 매개변수는 읽어들일 메시지의 범위를 지정, 잘 쓰이지는 않으므로 자세히는 안다룸
        1. TranslateMessage(&msg); : 키보드 입력메시지
        2. DispatchMessage(&msg); : 시스템 큐에서 꺼내고 형태를 조금 바꾼 뒤 메시지를 프로그램의 메시지 핸들러 함수(WndProc)로 전달
    6. return msg.wParam;
        1. 메시지 루프가 종료되면 프로그램은 Message.wParam을 리턴하고 종료(WM_QUIT 메시지로부터 전달된 코드)
- **WinProc(callback 함수)** : switch문을 이용해 발생하는 메시지에 따라 표시
        `LRESULT CALLBACK WndProc(HWND hwnd, UINT imessage, WPARAM wParam, LPARAM lParam);`
    - hwnd : 메시지가 전달될 윈도우 핸들값
    - imessage : 메시지의 종류
    - wParam, lParam :메시지와 관련된 부가적인 정보가 전달됨
        `switch (imessage) {`
        
        1. WM_PAINT:
            ```cpp
            		PAINTSTRUCT ps;
            		HDC hdc = BeginPaint(hWnd, &ps);
            		EndPaint(hWnd, &ps);
            		return 0;
            ```
        - DC(Device Contest) : 데이터 구조체, 윈도우에서는 DC를 통해 출력을 해결함. 윈도우 DC, 프린터 DC, 화면 DC가 제각각 필요
        - 문자열 출력은 TextOut 함수(dos의 printf함수)
        - PAINTSTRUCT : 윈도우 클라이언트 영역에 무언가를 그리려고 할 때 필요한 정보를 담고 있는 구조체
            1. 운영체제에 DC를 요청
            2. 운영체제가 제공한 DC를 매개변수로 하는 API를 호출하여 출력
            3. DC 사용이 끝났음을 운영체제에 알리고 반납

2. WM_CREATE:
    
    1. 차일드 윈도우 생성할때 주로 쓰는 듯?
3. WM_DESTROY:
    
    ```cpp
            PostQuitMessage(0);
            return 0;
    ```
    
4. `return DefWindowProc(hWnd, mesg, wParam, lParam);`
    
    WndProc에서 처리하지 않은 나머지 메시지에 관한 처리를 해주는 함수
            
- 차일드 윈도우
        
1. 형태 : 1️⃣컨트롤 2️⃣일반 윈도우

컨트롤 같이 윈도우 클래스가 이미 등록되어 있으면 새로 등록할 필요❌

차일드 윈도우는 정수값 ID가 필요, 버튼은 매크로를 이용해 정의해두는 듯?

2. 일반 윈도우

1. ChildWnd : 1️⃣정의 2️⃣등록 3️⃣생성(Create) 4️⃣Show
2. ChildProc : WinProc와 동일
3. 컨트롤

- 생성(Create)만 해서 사용하면 됨
    
- 정의된 윈도우 클래스
    
    윈도우 클래스
    
    button
    
    static
    
    scrollbar
    
    edit
    
    listbox
    
    combobox
    
    컨트롤
    
    버튼, 체크, 라디오
    
    텍스트
    
    스크롤바
    
    에디터
    
    리스트 박스
    
    콤보 박스
    
- 이벤트 발생시 부모 윈도우에 통지 메시지(Notification Message)를 보냄
    
- 파라메타 : 통지메시지로 함께 전달되는 정보
    
    매개변수
    
    의미
    
    wParam
    
    상위 2바이트 : 부모 윈도우에 알려주는 이벤트 메시지
    
    하위 2바이트 : 윈도우나 컨트롤 ID
    
    lParam
    
    버튼 컨트롤의 윈도우 핸들
    
    HWORD(wParam)
    
    상위 2바이트 값, 이벤트 메시지처리과정은 교재 4장(MDI)부터
    
    LOWORD(wParam)
    
    하위 2바이트 값, 윈도우의 ID
                
- **WinMain, WinProc 더 자세한 흐름**
        
    - WinMain 윈도우 메인 함수
            
        - 윈도우 클래스 정의 : WND CLASS
                
            WndClass의 각 멤버 의미
            
            style
            
            윈도우의 스타일을 정의
            
            lpfn WndProc
            
            윈도우의 메시지 핸들러 함수를 지정
            
            cdClsExtra, cbWndExtra
            
            일종의 예약 영역
            
            hinstance
            
            이 윈도우 클래스를 사용하는 프로그램의 번호이며 매개변수로 전달된 hInstance값을 그대로 대입해주면 된다.
            
            hicon, hcursor
            
            이 윈도우가 사용할 마우스 커서와 최소화되었을 경우 출력될 아이콘을 지정한다.
            
            hberbackground
            
            윈도우의 배경 색상을 지정
            
            lpszMenuname
            
            프로그램이 사용할 메뉴 지정, 리소스에디터로 별도로 만든 후 링크시에 합쳐짐
            
            예시 : WndClass.lpszMenuName=MAKEINTRESOURCE(메뉴리소스이름);
            
            lpszclassname
            
            윈도우 클래스의 이름 정의
            
            ```cpp
            WNDCLASS WndClass;
            g_hInst = hInstance;
            
            WndClass.cbClsExtra = 0;
            WndClass.cbWndExtra = 0;
            WndClass.hbrBackground = (HBRUSH)GetStockObject(WHITE_BRUSH);
            WndClass.hCursor = LoadCursor(NULL, IDC_ARROW);
            WndClass.hIcon = LoadIcon(NULL, IDI_APPLICATION);
            WndClass.hInstance = hInstance;
            WndClass.lpfnWndProc = (WNDPROC)WndProc;
            WndClass.lpszClassName = lpszClass;
            WndClass.lpszMenuName = NULL;
            WndClass.style = CS_HREDRAW | CS_VREDRAW;
            RegisterClass(&WndClass);     //메인윈도우 클래스 등록
            
            WndClass.lpfnWndProc = ChildWndProc;      //차일드 윈도우 프로시저
            WndClass.lpszClassName = ChildClassName; //차일드 윈도우 클래스이름
            RegisterClass(&WndClass);
            ```
                
        - 윈도우 클래스 등록 : Register Class()
                
            ```cpp
            RegisterClass(&WndClass);
            ```
                
        - 윈도우 객체 생성 : Create Window()
                
            매개 변수
            
            lpszClassName
            
            윈도우의 클래스를 지정하는 문자열
            
            lpszWindowName
            
            윈도우의 타이틀 바에 나타날 문자열
            
            dwStyle
            
            윈도우의 형태를 지정하는 매개변수WS_OVERLAPPEDWINDOW를 사용하면 시스템 메뉴, 최대 최소 버튼, 타이틀 바, 경계선을 가진 윈도우를 만들어 준다.
            
            X, Y, nWidth, nHeight
            
            윈도우의 크기와 위치를 지정하며 픽셀 단위를 사용한다. x, y좌표는 윈도우의 좌상단 좌표이며 nWidth는 넓이, nHeight는 높이이다.
            
            hWndParent
            
            부모 윈도우가 있을 경우 부모 윈도우의 핸들이다.
            
            hmenu
            
            윈도우에서 사용할 메뉴의 핸들을 지정한다.
            
            hinst
            
            윈도우를 만드는 주체, 즉 프로그램의 핸들을 지정한다. 여기서는 매개변수로 전달된 hInstance이다.
            
            lpvParam
            
            CREATESTRUCT라는 구조체의 번지이며 특수한 목적에 사용된다. 보통은 NULL값을 사용한다.
                
        - 화면에 윈도우 표시 : show Window()
                
            매개 변수
            
            SW_HIDE
            
            윈도우를 숨긴다.
            
            SW_MINIMIZE
            
            윈도우를 최소화시키고 활성화시키지 않는다.
            
            SW_RESTORE
            
            윈도우를 활성화시킨다
            
            SW_SHOW
            
            윈도우를 활성화시켜 보여준다.
            
            SW_SHOWNORMAL
            
            윈도우를 활성화시켜 보여준다.
                
        - 메시지 루프 : 사용자로부터 메시지 처리
                
            ```cpp
            while (GetMessage(&Message, 0, 0, 0)) {
                    TranslateMessage(&Message);
                    DispatchMessage(&Message);
                }
            ```
            
            1. BOOL GetMessage( );이 함수는 시스템이 유지하는 메시지 큐에서 메시지를 읽어 들인다.
                
            2. BOOL TranslateMessage( CONST MSG *lpMsg); 키보드 입력 메시지를 가공하여 프로그램에서 쉽게 쓸 수 있도록 해 준다.
                
            3. LONG DispatchMessage( CONST MSG *lpmsg);시스템 메시지 큐에서 꺼낸 메시지를 프로그램의 메시지 핸들러 함수(WndProc)로 전달한다.
                
            4. MSG구조체실제 메시지 처리는 메시지 처리 함수인 콜백함수(WndProc)에서 수행한다. 메시지는 MSG라는 구조체에 보관되며 MSG 구조체 각 멤버의 역할은 다음과 같다.
                
                ① Hwnd : 메시지를 받을 윈도우 핸들이다.
                
                ② message : 어떤 종류의 메시지인가를 나타낸다. 가장 중요한 값이다.
                
                ③ wParam : 전달된 메시지에 대한 부가적인 정보를 가진다. 어떤 의미를 가지는가는 메시지 별로 다르다. 32비트 값이다.
                
                ④ lParam : 전달된 메시지에 대한 부가적인 정보를 가진다. 어떤 의미를 가지는가는 메시지 별로 다르다. 32비트 값이다.
                
                ⑤ Time : 메시지가 발생한 시간이다.
                
                ⑥ Pt : 메시지가 발생했을 때의 마우스 위치이다.
                    
    - WndProc(Window Proc) 윈도우 프로시저(=CALLBACK함수라고 불림)
            
        > 이벤트 발생 → 메시지 → 시스템 메시지 큐 → (Post Message) → 응용 프로그램 큐 → winMain(){메시지 루프} → 운영체제 → WndProc(){윈도우 프로시저}에 send Message ⇒ 디폴트 윈도우 프로시저
            
        - 메시지 핸들러 함수로 메시지가 발생할 때 프로그램의 반응을 처리
                
        - 윈도우 운영체제에 의해 호출되어 메시지를 처리한다. 이렇게 운영체제에 의해 호출되는 응용 프로그램내의 함수를 콜백(CallBack)함수라고 함
                
        - 콜백(Callback) 함수 또는 윈도우 프로시저 함수 WndProc의 구조는 대체로 다음과 같은 형태를 가진다. 메시지의 종류에 따라 다중 분기하여 메시지 별로 처리를 진행한다.
                
            ```cpp
            switch(iMessage){
                case Msg1:처리1;return 0;case Msg2:처리2;return 0;...
                case WM_DESTROY:PostQuitMessage(0);
                return 0;
            }
            return(DefWindowProc(hWnd,iMessage,wParam,lParam));}
            ```
## 2. 실제 코드 
 - **코드실행시 실행화면**![[Pasted image 20221017204623.png]]
    적어둔 코드에서 눈여겨볼 것
- 클래스 상속, 생성자
- 윈도우 클래스 2개 생성, 버튼 클릭시 사이트이동&차일드 윈도우 표시, 리소스에디터를 이용해 메뉴창 생성, Message 창에 인포메이션 아이콘 추가

- student.h
        
    ```cpp
    #pragma once
    #include <Windows.h>
    
    class CPerson 
    {
    public:
        LPCTSTR m_pName;
        int m_Age;
        CPerson(LPCTSTR pName, int age);
        void print(HDC hdc, int x, int y);
    };
    
    class CStudent: public CPerson 
    {
        //멤버변수
        int m_Number;
        int m_Grade;
    
    public:
        //멤버함수
        CStudent(LPCTSTR pName, int age, int num);
        void print(HDC hdc, int x, int y);
    };
    ```
- student.cpp
        
    ```cpp
    #include "student.h"
    CPerson::CPerson(LPCTSTR pName, int age)
    {
        m_pName = pName;
        m_Age = age;
    };
    
    CStudent::CStudent(LPCTSTR pName, int age, int num): CPerson(pName,age)
    {
        m_pName = pName;
        m_Age = age;
        m_Number = num;
    };
    
    void CStudent::print(HDC hdc, int x, int y) 
    {
        TCHAR buf[256];
        wsprintf(buf, L"<이름> : %s, <나이> : %d, <학번> : %d", m_pName, m_Age, m_Number);
        TextOut(hdc, x, y, buf, lstrlen(buf));
    };
    ```
- HelloAPI.cpp
        
    ```cpp
    #include "student.h"
    #include "resource.h"
    
    #define child_button 3000
    #define child_button2 4000
    
    HINSTANCE g_hInst;
    HINSTANCE g_link;
    
    LPCTSTR szAppName = L"HelloAPI";
    LPCTSTR childszAppName = L"HelloAPIchild";
    LPCTSTR szAppName2 = L"HelloAPI2";
    
    //원형 선언 
    LRESULT CALLBACK WndProc(HWND, UINT, WPARAM, LPARAM);
    LRESULT CALLBACK childWndProc(HWND, UINT, WPARAM, LPARAM);
    LRESULT CALLBACK WndProc2(HWND, UINT, WPARAM, LPARAM);
    
    //-------------------------------
    int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpszArg, int nCmdShow)
    {
        //윈도우 생성
        HWND hWnd;
        MSG msg;
        g_hInst = hInstance;
        WNDCLASS WndClass; //객체생성(인스턴스)
    
        WndClass.style = CS_HREDRAW | CS_VREDRAW;
        WndClass.lpfnWndProc = (WNDPROC)WndProc;
        WndClass.cbClsExtra = 0;
        WndClass.cbWndExtra = 0;
        WndClass.hInstance = hInstance;
        WndClass.hIcon = LoadIcon(NULL, IDI_APPLICATION);
        WndClass.hCursor = LoadCursor(NULL, IDC_ARROW);
        WndClass.hbrBackground = (HBRUSH)GetStockObject(WHITE_BRUSH);  //배경색 지정
        WndClass.lpszMenuName = MAKEINTRESOURCE(IDR_MENU1);
        WndClass.lpszClassName = szAppName;
        if (!RegisterClass(&WndClass)) return NULL; //윈도우 클래스 등록
    
        //차일드 윈도우
        WndClass.lpszClassName = childszAppName;
        WndClass.lpfnWndProc = childWndProc;
        if (!RegisterClass(&WndClass)) return NULL; //윈도우 클래스 등록
    
        //윈도우2 생성
        HWND hWnd2;
        MSG msg2;
        WNDCLASS WndClass2;
    
        WndClass2.style = CS_HREDRAW | CS_VREDRAW;
        WndClass2.lpfnWndProc = WndProc2;
        WndClass2.cbClsExtra = 0;
        WndClass2.cbWndExtra = 0;
        WndClass2.hInstance = hInstance;
        WndClass2.hIcon = LoadIcon(NULL, IDI_APPLICATION);
        WndClass2.hCursor = LoadCursor(NULL, IDC_ARROW);
        WndClass2.hbrBackground = (HBRUSH)GetStockObject(WHITE_BRUSH);  //배경색 지정
        WndClass2.lpszMenuName = MAKEINTRESOURCE(IDR_MENU1);
        WndClass2.lpszClassName = szAppName2;
        if (!RegisterClass(&WndClass2)) return NULL; //윈도우 클래스 등록
    
        hWnd = CreateWindow(szAppName,
            L"1번째",
            WS_OVERLAPPEDWINDOW,
            300,100,
            500,400,
            (HWND)NULL,
            (HMENU)NULL,
            hInstance,
            NULL
        );
    
        hWnd2 = CreateWindow(szAppName2,
            L"2번째",
            WS_OVERLAPPEDWINDOW,
            800,100,
            400,200,
            (HWND)NULL,
            (HMENU)NULL,
            hInstance,
            NULL
        );
    
        ShowWindow(hWnd, nCmdShow);  // 윈도우를 화면에 보이게 하는 역활
        UpdateWindow(hWnd);  // 윈도우를 화면에 보이게 하는 역활
    
        ShowWindow(hWnd2, nCmdShow);  // 윈도우를 화면에 보이게 하는 역활
        UpdateWindow(hWnd2);  // 윈도우를 화면에 보이게 하는 역활
    
        while (GetMessage(&msg, NULL, 0, 0))
        {
            TranslateMessage(&msg);
            DispatchMessage(&msg);
        }
        return msg.wParam;
        // 이벤트가 발생할 때마다 윈도우즈가 자동으로 호출한다
    }
    
    //-------------------------------
    LRESULT CALLBACK WndProc(HWND hWnd, UINT mesg, WPARAM wParam, LPARAM lParam) //이벤트 실행
    {
        switch (mesg)	{
        case WM_PAINT: {
            PAINTSTRUCT ps;
            HDC hdc = BeginPaint(hWnd, &ps);
            EndPaint(hWnd, &ps);
            return 0;
        }
        case WM_CREATE : {
            HWND hChildWnd = CreateWindow(
                L"button",        		// 윈도우 클래스 이름 
                L"버튼 1",		// 윈도우 타이틀 
                WS_CHILD | WS_VISIBLE, 	// 윈도우 스타일 
                10,	70, 		 // 윈도우 보일 때 x, y 좌표 
                100, 30,
                hWnd,         		// 부모 윈도우
                (HMENU)child_button,   	// 컨트롤 ID
                g_hInst,           		// 인스턴스 핸들 
                (LPVOID)NULL);      	// 여분의 데이터
    
            hChildWnd = CreateWindow(
                L"button",        		// 윈도우 클래스 이름 
                L"버튼 2",		// 윈도우 타이틀 
                WS_CHILD | WS_VISIBLE, 	// 윈도우 스타일 
                120, 70,			 // 윈도우 보일 때 x, y 좌표 
                100, 30,
                hWnd,         		// 부모 윈도우
                (HMENU)child_button2,   	// 컨트롤 ID
                g_hInst,           		// 인스턴스 핸들 
                (LPVOID)NULL);      	// 여분의 데이터
    
            if (!hChildWnd) 	return -1;
            return 0;
            }
        case WM_COMMAND: {
            switch (LOWORD(wParam))
            {
            case child_button:
                g_link = ShellExecute(hWnd, L"open", L"<https://www.knou.ac.kr/>", L"", L"", SW_SHOWDEFAULT);
                break;
            case child_button2: //버튼2 클릭시 차일드 윈도우 표시 
                HWND hChildWnd = CreateWindow(
                    childszAppName,     		// 차일드 윈도우 클래스 이름 
                    L"차일드 윈도우",            	// 윈도우 타이틀 
                    WS_OVERLAPPEDWINDOW | WS_CHILD | WS_VISIBLE,  // 윈도우  스타일 
                    240, 40,        		// 윈도우 보일 때 x, y 좌표 
                    230, 280,      		// 윈도우 폭, 높이
                    hWnd,         		// 부모 윈도우
                    (HMENU)1000,        	// 차일드 윈도우ID 
                    g_hInst,           		// 인스턴스 핸들 
                    (LPVOID)NULL);      	// 여분의 데이터			
                break;
            }
            return 0;
        }
        case WM_DESTROY:  //끝?
            PostQuitMessage(0);
            return 0;
        }
        return DefWindowProc(hWnd, mesg, wParam, lParam);
    }
    LRESULT CALLBACK childWndProc(HWND hWnd, UINT mesg, WPARAM wParam, LPARAM lParam)
    {
        switch (mesg)
        {
        case WM_PAINT: {
            PAINTSTRUCT ps;
            HDC hdc = BeginPaint(hWnd, &ps);
            EndPaint(hWnd, &ps);
            return 0;
        }
        case WM_CREATE: {
            HWND hChildWnd = CreateWindow(
                L"button",        		// 윈도우 클래스 이름 
                L"버튼 1",		// 윈도우 타이틀 
                WS_CHILD | WS_VISIBLE, 	// 윈도우 스타일 
                10, 70, 		 // 윈도우 보일 때 x, y 좌표 
                80, 30,
                hWnd,         		// 부모 윈도우
                (HMENU)child_button,   	// 컨트롤 ID
                g_hInst,           		// 인스턴스 핸들 
                (LPVOID)NULL);      	// 여분의 데이터
    
            hChildWnd = CreateWindow(
                L"button",        		// 윈도우 클래스 이름 
                L"버튼 2",		// 윈도우 타이틀 
                WS_CHILD | WS_VISIBLE, 	// 윈도우 스타일 
                120, 70,			 // 윈도우 보일 때 x, y 좌표 
                80, 30,
                hWnd,         		// 부모 윈도우
                (HMENU)child_button2,   	// 컨트롤 ID
                g_hInst,           		// 인스턴스 핸들 
                (LPVOID)NULL);      	// 여분의 데이터
    
            if (!hChildWnd) 	return -1;
            return 0;
        }
        case WM_COMMAND: {
            if (LOWORD(wParam) == child_button) {
                MessageBox(hWnd, L"버튼1이 클릭되었다", L"버튼1", MB_OK | MB_ICONINFORMATION);
            }
            if (LOWORD(wParam) == child_button2) {
                MessageBox(hWnd, L"버튼2이 클릭되었다", L"버튼2", MB_OK | MB_ICONINFORMATION);
            }
            return 0;
        }
        }
        return DefWindowProc(hWnd, mesg, wParam, lParam);
    
    }
    
    //-------------------------------
    LRESULT CALLBACK WndProc2(HWND hWnd2, UINT mesg, WPARAM wParam, LPARAM lParam) //이벤트 실행
    {
        LPCTSTR text = L"메인 윈도우";
    
        switch (mesg)
        {
        case WM_PAINT :{
            PAINTSTRUCT ps;
            HDC hdc = BeginPaint(hWnd2, &ps);
            TextOut(hdc, 10, 10, text, lstrlen(text));
            CStudent newStudent(L"홍길동", 20, 202013);
            newStudent.print(hdc, 10, 50);
            EndPaint(hWnd2, &ps);
            return 0;
            }
        }
        return DefWindowProc(hWnd2, mesg, wParam, lParam);
    }
    ```


# MFC
- MDI
- SDI