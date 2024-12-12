# 실습 2

-------

대화 상자 기반 프로젝트 생성 후

Group Box를 만들고 속성을 설정한다.

![image](https://github.com/user-attachments/assets/805d6e75-ac92-4f97-931d-c4bd4a1efae3)

| ID | 캡션 | 읽기 전용 | 텍스트 맞춤 | 정렬 | 테두리 |
|---|---|---|---|---|---|
| IDC_RADIO_LENGTH | 길이 | | | | |
| IDC_RADIO_WEIGHT | 무게 | | | | |
| IDC_BUTTON_UNIT_VIEW | 변환 단위표 | | | | |
| IDC_EDIT_UNIT | | True | Center | | |
| IDC_LIST_PERSENT_UNIT | | | | False | |
| IDC_LIST_CHANGE_UNIT | | | | False | |
| IDC_STATIC8 | 현재 값 | | | | | |
| IDC_STATIC9 | 변환된 값 | | | | | |
| IDC_EDIT_PERSENT_VALUE | | | Right | | | |
| IDC_EDIT_PERSENT_UNIT | | True | | | | False |
| IDC_EDIT_CHANGE_VALUE | | | True | Right | | |
| IDC_EDIT_CHANGE_UNIT | | True | | | | False |
| IDC_STATIC10 | = | | | | |

다음과 같이 설정하면 아래 처럼 된다.

![image](https://github.com/user-attachments/assets/e99007c5-51d3-4cb6-9370-a4c26cf6dbf5)

그 후 클래스 마법사 실행후 [멤버 변수] 탭에서 다음과 같이 설정한다.

| 컨트롤 ID | 범주 | 이름 | 변수 형식 |
|---|---|---|---|
| IDC_EDIT_PERSENT_VALUE | 값 | m_dPersentValue | double |
| IDC_EDIT_CHANGE_VALUE | 값 | m_dChangeValue | double |
| IDC_EDIT_PERSENT_UNIT | 값 | m_strPersnetUnit | CString |
| IDC_EDIT_CHANGE_UNIT | 값 | m_strChangeUnit | CString |
| IDC_EDIT_UNIT | 값 | m_strUnit | CString |
| IDC_LIST_PERSENT_UNIT | 컨트롤 | m_listPresentUnit | CListBox |
| IDC_LIST_CHANGE_UNIT | 컨트롤 | m_listChangeUnit | CListBox |

[클래스 뷰] 에서 Cmessage2DIg 클래스 선택 후 변수 추가하여 자료형을 int 로 선언하고 변수 이름은 m_nUnitSelect로 한다.

그 후 [ 명령 ] 탭 에서 [ 개체 ID ] 항목에서 IDC_RADIO_LENGTH를 선택 후 COMMAND 메시지를 선택하여 메시지 핸들러 함수를 추가한다.<br>
그리고 다음과 같은 코드를 작성한다.

```ruby
void Cmessage2Dlg::OnRadioLength()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	m_nUnitSelect = 1;
	m_listPresentUnit.ResetContent(); //왼쪽 List box 아이템 삭제
	m_listChangeUnit.ResetContent(); //오른쪽 List box 아이템 삭제
	m_strUnit.Empty();
	m_dPersentValue = m_dChangeValue = 0;

	m_listPresentUnit.AddString(_T("미터(m)")); //왼쪽 List box 아이템 생성
	m_listPresentUnit.AddString(_T("인치(in)"));
	m_listPresentUnit.AddString(_T("야드(yd)"));

	m_listChangeUnit.AddString(_T("미터(m)")); //오른쪽 List box 아이템 생성
	m_listChangeUnit.AddString(_T("인치(in)"));
	m_listChangeUnit.AddString(_T("야드(yd)"));

	m_listPresentUnit.SetCurSel(0); //왼쪽 List Box 첫 번째 아이템 선택
	m_listChangeUnit.SetCurSel(0); //오른쪽 List Box 첫 번째 아이템 선택
	m_strUnit = m_strUnit + _T("미터(m) --> 미터(m)"); //변환될 단위 문자열 생성
	m_strPresentUnit = _T("m");
	m_strChangeUnit = _T("m");
	UpdateData(FALSE);
}
```

그리고 같은 방법으로 무게 라디오 버튼에 해당하는 메시지 핸들러 함수 추가하고 다음과 같은 코드 작성한다.

```ruby
void Cmessage2Dlg::OnRadioWeigth()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	m_nUnitSelect = 2;
	m_listPresentUnit.ResetContent(); //왼쪽 List box 아이템 삭제
	m_listChangeUnit.ResetContent(); //오른쪽 List box 아이템 삭제
	m_strUnit.Empty();
	m_dPersentValue = m_dChangeValue = 0;

	m_listPresentUnit.AddString(_T("그램(g)")); //왼쪽 List box 아이템 생성
	m_listPresentUnit.AddString(_T("온즈(oz)"));
	m_listPresentUnit.AddString(_T("파운드(lb)"));

	m_listChangeUnit.AddString(_T("미터(m)")); //오른쪽 List box 아이템 생성
	m_listChangeUnit.AddString(_T("온즈(oz)"));
	m_listChangeUnit.AddString(_T("파운드(lb)"));

	m_listPresentUnit.SetCurSel(0); //왼쪽 List Box 첫 번째 아이템 선택
	m_listChangeUnit.SetCurSel(0); //오른쪽 List Box 첫 번째 아이템 선택
	m_strUnit = m_strUnit + _T("그램(g) --> 그램(g)"); //변환될 단위 문자열 생성
	m_strPresentUnit = _T("g");
	m_strChangeUnit = _T("g");
	UpdateData(FALSE);
}
```

그 후 Cmessage2DIg 에 함수를 추가해준다

![image](https://github.com/user-attachments/assets/15f5d2e9-1955-41bd-aa29-d30934b92b0f)

그리고 여기에 List Box에서 현재 단위와 변환하려는 단위를 선택하고 Edit Control에 현재 값을 입력하면 변환된 값으로 게산하는 함수를 구현한다.

```ruby
void Cmessage2Dlg::ComputeUnitValue()
{
	// TODO: 여기에 구현 코드 추가.
	UpdateData(TRUE); //Edit Control부터 입력한 값을 가져온다.
	int index1, index2;
	index1 = m_listPresentUnit.GetCurSel();
	index2 = m_listChangeUnit.GetCurSel();
	m_dChangeValue = m_dPersentValue;

	switch (m_nUnitSelect)
	{
	case 1:
		if (index1 == 0 && index2 == 1) //미터에서 인치
			m_dChangeValue = m_dPersentValue * 39.370079;
		if (index1 == 0 && index2 == 2) //미터에서 야드
			m_dChangeValue = m_dPersentValue * 1.093613;
		if (index1 == 1 && index2 == 0) //인치에서 미터
			m_dChangeValue = m_dPersentValue * 0.0254;
		if (index1 == 1 && index2 == 2) //인치에서 야드
			m_dChangeValue = m_dPersentValue * 0.027778;
		if (index1 == 2 && index2 == 0) //야드에서 미터
			m_dChangeValue = m_dPersentValue * 0.9144;
		if (index1 == 2 && index2 == 1) //야드에서 인치
			m_dChangeValue = m_dPersentValue * 36;
		break;
	case 2:
		if (index1 == 0 && index2 == 1) //그램에서 온즈
			m_dChangeValue = m_dPersentValue * 0.035274;
		if (index1 == 0 && index2 == 2) //그램에서 파운드
			m_dChangeValue = m_dPersentValue * 0.002205;
		if (index1 == 1 && index2 == 0) //온즈에서 그램
			m_dChangeValue = m_dPersentValue * 28.349523;
		if (index1 == 1 && index2 == 2) //온즈에서 파운드
			m_dChangeValue = m_dPersentValue * 0.0625;
		if (index1 == 2 && index2 == 0) //파운드에서 그램
			m_dChangeValue = m_dPersentValue * 0.0625;
		if (index1 == 2 && index2 == 1) //파운드에서 온즈
			m_dChangeValue = m_dPersentValue * 16;
		break;
	default:
		AfxMessageBox(_T("변환하고자 하는 단위를 라디오 버튼에서 선택하세요."));
	}
	UpdateData(FALSE); //Edit Control부터 결과 값을 보낸다.
}
```

그 후 Edit Control 에 대한 메시지 핸들러를 만들기 위해

클래스 마법사를 실행시캬 [명령] 탭 [객체 ID] 항목에서 IDC_EDIT_PRESENT_VALUE를 선택하고 [메시지] 항목은 EN_CHANGE 메시지를 선택하여 메시지 핸들러 함수를 추가한 후 코드를 입력한다.

```ruby
	void Cmessage2Dlg::OnChangeEditPersentValue()
	{
		// TODO:  RICHEDIT 컨트롤인 경우, 이 컨트롤은
		// CDialogEx::OnInitDialog() 함수를 재지정 
		//하고 마스크에 OR 연산하여 설정된 ENM_CHANGE 플래그를 지정하여 CRichEditCtrl().SetEventMask()를 호출하지 않으면
		// ENM_CHANGE가 있으면 마스크에 ORed를 플래그합니다.

		// TODO:  여기에 컨트롤 알림 처리기 코드를 추가합니다.
		ComputeUnitValue();
	}
```

그 후 List Box에 대한 메시지 핸들러 함수를 만들기 위해

클래스 마법사를 실행시켜 [명령] 탭 [객체 ID] 항목에서 IDC_LIST_PRESENT_UNIT를 선택하고 [메시지] 항목은 LBN_SELCHANGE 메시지를 선택하여 메시지 핸들러 함수를 추가한 후 코드를 입력한다.

```ruby
	void Cmessage2Dlg::OnSelchangeListPersentUnit()
	{
		// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
		int index1, index2;
		index1 = m_listPresentUnit.GetCurSel();
		index2 = m_listChangeUnit.GetCurSel();
		CString strPresentUnit, strChangeUnit;
		m_strUnit.Empty();

		if (m_nUnitSelect == 1) {
			switch (index1) {
			case 0:
				m_strPresentUnit = _T("m");
				break;
			case 1:
				m_strPresentUnit = _T("in");
				break;
			case 2:
				m_strPresentUnit = _T("yd");
				break;
			}
		}
		else if (m_nUnitSelect == 2) {
			switch (index1)
			{
			case 0:
				m_strPresentUnit = _T("g");
				break;
			case 1:
				m_strPresentUnit = _T("oz");
				break;
			case 2:
				m_strPresentUnit = _T("lb");
				break;
			}
		}
		m_listPresentUnit.GetText(index1, strPresentUnit);
		m_listChangeUnit.GetText(index2, strChangeUnit);
		m_strUnit = m_strUnit + strPresentUnit + _T(" --> ") + strChangeUnit;

		UpdateData(FALSE);
		ComputeUnitValue();
	}
```

그리고 나서 위와 같은 방식으로 오른쪽 List Box에 대한 메시지 핸들러 함수를 추가하고 다음과 같이 코드를 입력한다.

```ruby
	void Cmessage2Dlg::OnSelchangeListChangeUnit()
	{
		// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
		int index1, index2;
		index1 = m_listPresentUnit.GetCurSel();
		index2 = m_listChangeUnit.GetCurSel();
		CString strPresentUnit, strChangeUnit;
		m_strUnit.Empty();

		if (m_nUnitSelect == 1) {
			switch (index1) {
			case 0:
				m_strChangeUnit = _T("m");
				break;
			case 1:
				m_strChangeUnit = _T("in");
				break;
			case 2:
				m_strChangeUnit = _T("yd");
				break;
			}
		}
		else if (m_nUnitSelect == 2) {
			switch (index1)
			{
			case 0:
				m_strChangeUnit = _T("g");
				break;
			case 1:
				m_strChangeUnit = _T("oz");
				break;
			case 2:
				m_strChangeUnit = _T("lb");
				break;
			}
		}
		m_listPresentUnit.GetText(index1, strPresentUnit);
		m_listChangeUnit.GetText(index2, strChangeUnit);
		m_strUnit = m_strUnit + strPresentUnit + _T(" --> ") + strChangeUnit;

		UpdateData(FALSE);
		ComputeUnitValue();
	}
```

그리고 나서 변환 단위표를 열람할 수 있는 모덜리스(Modaless) 대화상자를 생성한다.

[리소스 뷰]의 Dialog에서 오른쪽 마우스 버튼을 눌러서 나타나는 단축 메뉴에서 [삽입] 항목을 선택한다.

ID를 IDD_DIALOG_UNIT_TABLE로 설정하고 캡션을 변환 단위표로 설정한다.
