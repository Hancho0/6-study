# 6주차 Study [ 2024-12-08 ~ 2024-12-13 ]

**[ 목표 ]**
- 이번주 목표 : 대화 상자 (대화상자 기반 프로젝트) 배우기
-----

**[ 진행 사항 ]**

대화상자는 사용자와 윈도우 간의 인터페이스 기능을 한다. 애플리케이션을 다루는 사용자는 이 대화상자를 통해서, 애플리케이션과 대화를 할 수 있다. 대화상자로만 구성된 애플리케이션에서도 SDI나 MDI에서 했던 기능들을 처리할 수 있다.

* 대화상자 기반의 프로젝트 클래스 구성 형태

| 클래스 | 기저 클래스 | 설명 |
|---|---|---|
| 애플리케이션 클래스 | CWinApp | 프로젝트 전체를 관리하는 클래스 |
| 대화상자 클래스 | CDialogEx | 대화상자의 기능을 구현하는 실제적인 클래스 |
| 도움말 대화상자 클래스 | CDialogEx | 도움말 정보 클래스 |

* MFC 기본 컨트롤

1) Static Text<br>
화면에 문자열을 배치할 때 사용하며 사용자로부터 명령을 받아들이지도 않고 출력을 내보내지도 않는다. 일반적으로 레이블(Label) 용도로 사용한다.

2) Edit Control<br>
문자열을 입력하고 편집할 수 있도록 해주는 컨트롤로 주로 사용자에게 문자열을 입력받을 때 사용된다. 간단한 컨트롤이지만 내부에는 문자열을 편집할 수 있는 키보드 단축키까지 완벽히 갖춰져 있을 정도로 고성능 컨트롤이다.

3) Group Box<br>
서로 연관된 컨트롤들을 시각적으로 그룹을 지어 다른 컨트롤과 구분하는 용도로 사용한다. 컨트롤을 Group Box로 묶는다고 기능이 달라지지는 않는다.

4) Button Control<br>
마우스로 클릭하여 어떤 동작을 수행하는 용도로 사용한다.

5) Check Box<br>
Button Control의 일종이며 마우스로 클릭하면 체크 표시가 on/off 된다. 여러 옵션 중에 임의의 개수를 선택할 때 주로 사용하되 독립적인 옵션을 선택한다.

6) Radio Button<br>
Button Control의 일종이며 마우스로 클릭하면 라디오 표시가 on/off 된다. 여러 옵션중에 하나만 선택하는 컨트롤로 하나를 선택하면 다른 것이 선택 해제되는 상호 배타적인 옵션을 선택한다.

7) List Box<br>
사용자가 선택할 수 있는 항목들을 여러 개 나열해 두고 선택할 수 있도록 해주는 컨트롤이다. 여기서 항복은 문자열이나 비트맵이 될 수 있다. List Box는 스타일에 따라 하나 혹은 여러 개 항목을 선택할 수 있다. 선택해야 할 대상을 키보드로 직접 입력해 주어야 하는 전통적인 방법보다 선택 대상을 보여주고 마우스로 간단히 선택할 수 있도록 하는 더욱 편리한 방법을 제공해 준다.

8) Combo Box<br>
List Box의 단점을 해결한 것이다 Combo Box이며 Edit Control과 List Box를 합쳐 놓은 모양이다. 기존의 항목을 선택할 때는 아래쪽의 List Box에서 선택하고 직접 입력해야 할 항목은 Edit Control에서 입력할 수 있으며 Combo Box는 필요할 때만 열어서 사용하고 평소에는 닫아 두기 때문에 화면 면적도 넓게 차지하지 않는다.

[ 실습 ]

대화상자 기반 프로젝트 생성 후

도구 상자 에서 Group Box 컨트롤을 선택하여 배치해준다.

그 후 다음과 같이 라디오 버튼, 체크 박스, 리스트 박스, 에디트 박스, 콤보 박스, 버튼을 배치해준다

그 후 각 이름 설정해주면서 ID 와 캡션을 설정해준다.

![1](https://github.com/user-attachments/assets/c840e379-9e35-440c-b42a-02497fdf420d)

그 후 리스트 박스 하고 콤보 박스에 변수를 추가해준다.

![2](https://github.com/user-attachments/assets/6db88bea-f875-407f-9ab0-4e9be3118fa6)
![3](https://github.com/user-attachments/assets/a1b07467-79d8-4227-907b-17222a03126c)

그 후 클래스뷰에서 CmessageDIg 에서 함수를 추가해준다.

![4](https://github.com/user-attachments/assets/7a24a95b-7480-44cd-85a3-c3511f73b658)

함수이름 UpdateComboBox 으로 하고 반환 형식은 void로 지정한다.

여기에 List Box의 아이템 수를 세어서 그 만큼 Combo Box에 "리스트 항목: n"이라는 문자열을 추가시키는 코드를 구현한다.
```ruby
void CmessageDlg::UpdateComboBox()
{
	// TODO: 여기에 구현 코드 추가.
	int nCnt = m_listBox.GetCount();
	m_cbListItem.ResetContent();

	for (int i = 0; i < nCnt; i++) {
		CString strItem;
		strItem.Format(_T("리스트 항목 %d"), i + 1);
		m_cbListItem.AddString(strItem);
	}
}
```

클래스 마법사 [개체 ID] 항목에서 IDC_RADIO1을 [메시지] 항목에서 COMMAND 메시지를 선택후 [처리기 추가] 버튼을 선택하면 다음과 같은 메시지 핸들러 함수를 추가한다는 대화상자가 출력된다.
[멤버 함수 추가] 대화상자에서 지정된 값으로 지정하고 [확인] 버튼을 눌러서 메시지 핸들러 함수를 추가한다.

```ruby
void CmessageDlg::OnRadio1()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	m_listBox.AddString(_T("1번 라디오 버튼 선택"));
	UpdateComboBox();
}
```

IDC_RADIO2 도 똑같이 해준다.

```ruby
void CmessageDlg::OnRadio2()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	m_listBox.AddString(_T("2번 라디오 버튼 선택"));
	UpdateComboBox();
}
```

CmessageDIg 클래스에 변수를 m_bChecked 로 하고 형식을 bool[2] 로 지정해준다.<br>
그러나 Visual Studio 2022 가 지속적으로 업데이트 진행하면서 형식을 지정해주면 에러 메시지가 출력된다<br>
그래서 bool 형식으로 잡고 헤더 파일 가서 bool m_bChecked[2]; 형식으로 잡아준다.<br>

그리고 앞에서 선언한 배열 변수를 추기화 하기 위해서 성성자 함수에 초기화 코드를 추가한다.
```ruby
CmessageDlg::CmessageDlg(CWnd* pParent /*=nullptr*/)
	: CDialogEx(IDD_MESSAGE_DIALOG, pParent)
	, m_strEdit(_T(""))
{
	m_hIcon = AfxGetApp()->LoadIcon(IDR_MAINFRAME);
	//변수 초기화
	m_bChecked[0] = m_bChecked[1] = FALSE;
}
```

그 후 클래스 마법사에서 IDC_CHECK1 항목에서 BN_CLICKED 메시지를 선택하고 처리기 추가 하여 메시지 핸들러 함수를 추가후 코드를 추가해준다.
```ruby
void CmessageDlg::OnClickedCheck1()
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
	if (m_bChecked[0] == FALSE)
	{
		m_bChecked[0] = TRUE;
		m_listBox.AddString(_T("1번 체크 박스 상태 TRUE"));
	}
	else
	{
		m_bChecked[0] = FALSE;
		m_listBox.AddString(_T("1번 체크 박스 상태 FALSE"));
	}
	UpdateComboBox();
}
```

IDC_CHECK2 항목도 똑같이 해준다.
```ruby
void CmessageDlg::OnClickedCheck2()
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
	if (m_bChecked[1] == FALSE)
	{
		m_bChecked[1] = TRUE;
		m_listBox.AddString(_T("2번 체크 박스 상태 TRUE"));
	}
	else
	{
		m_bChecked[1] = FALSE;
		m_listBox.AddString(_T("2번 체크 박스 상태 FALSE"));
	}
	UpdateComboBox();
}
```

IDC_BUTTON_ADD 메시지 항목에서 BN_CLICKED 에 메시지 핸들러 함수를 추가 후 아래 코드를 작성한다.
```ruby
void CmessageDlg::OnClickedButtonAdd()
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
	UpdateData(TRUE);
	if (m_strEdit.IsEmpty() == FALSE) {
		m_listBox.AddString(m_strEdit);
		m_strEdit.Empty();
	}
	else {
		AfxMessageBox(_T("에디트 상자에 문자열이 없습니다."));
	}
	UpdateData(FALSE);
	UpdateComboBox();
}
```
* UpdateData<br>
UpdateData() 함수의 파라미터가 TRUE일 때는 컨트롤의 데이터를 컨트롤과 연결된 멤버 변수로 가져오는 기능을 하며, 반대로 FALSE일 때는 컨트롤과 연결된 멤버 변수의 내용을 컨드롤에 세팅하는 기능을 한다.

그 후 IDC_BUTTON_INSERT 메시지 항목에서 BN_CLICKED 에 메시지 핸들러 함수를 추가한 후 아래 코드를 작성한다.
```ruby
void CmessageDlg::OnClickedButtonInsert()
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
	CString strSelText;
	int index = m_cbListItem.GetCurSel();
	if (index != CB_ERR) { //아이템이 선택되었을 경우
		m_listBox.GetText(index, strSelText);
		m_listBox.AddString(strSelText);
		UpdateComboBox();
	}
	else { //아이템이 선택되지 않았을 경우
		AfxMessageBox(_T("콤보 박스에서 삽입할 아이템을 선택하세요."));
	}
}
```

그 후 IDC_BUTTON_DELETE 에도 코드를 작성해준다.
```ruby
void CmessageDlg::OnClickedButtonDelete()
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
	int index = m_cbListItem.GetCurSel();
	if (index != CB_ERR) {
		m_listBox.DeleteString(index);
		UpdateComboBox();
	}
	else {
		AfxMessageBox(_T("콥보 박스에서 삭제할 아이템을 선택하세요."));
	}
}
```

[실행 결과]<br>
![5](https://github.com/user-attachments/assets/6aa6b38f-0235-419f-99b4-7b6f7c120bee)


[ 실습 2 ]<br>
https://github.com/Hancho0/6-study/blob/main/README2.md

-----
**[ 이번 Study를 통해 느낀점 ]**

되게 생각보다 쉽게 이해하면서 이번 스터디는 쉽게 했던거 같습니다. 좀더 응용해서 다른 프로그램도 만들어보고 싶다는 생각이 들어서 해볼려고 합니다 아직 좀 더 이해하지 못한 부분은 스스로 좀 더 찾아보면서 보완해 나갈 예정입니다.
