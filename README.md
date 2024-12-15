## ������� 1

### ������� 1. ��������������

��� ������ ������ __Web Module Federation__
* ���������� � ������������� ��������� ������ ���;
* � ������� ������������ React � ������� ����� ���� ������ �� ���;
* ������� ����� ����������:
	* �����
	* ������;
* ������������ ������������� �������������;
* �������� ���� �� ���������� (__lazy loading__);
* ��������� ������������ ������ ������ ��������� (������ �� ���������, �� � ��������� ������� ����� ���� �������������� �����, ����� ���������� ������ ������ �� ����� ����������� ����� �������� ��������� � ������);


### ������� 2. ������������ ���������
���������� �� ������

��� ���������� �� ������ ��������� ��������� __������������ �������__
* ����������� - ����������� ����� ������������� � ����������� ������������;
* ������� ������������;
* ���������� � �����;

����� �� ���� �������� � ��������� �������������, ���������� ������ ������ � ������������ � �����.
��� �������� ���������� � ������ ��������� �� ������ � ��������� ����������� � ��������� �������������

* ���� - ��� ���������� ������� __Web Module Federation__ 

���� (host)
~~~
/host
  /src
	/components
		App.js
		Footer.js
		Header.js
		Main.js
~~~

����������� (auth)
~~~
/auth
  /src
	/components
		InfoTooltip.js
		Login.js
		Register.js
	/unitls
		auth.js
~~~

������� ������������ (profile)
~~~
/profile
  /src
	/components
		EditAvatarPopup.js
		EditProfilePopup.js
~~~

����������� � ����� (card)
~~~
/card
  /src
	/components
		AddPlacePopup.js
		Card.js
		ImagePopup.js
		PopupWithForm.js
	/utils
		api.js
~~~


P.S. � ������� � JavaScript �� �������, ������ �������������� ���������, ������ �� ������� � �� ��������

## ������� 2

��������� � ����� ������� /arch_task2_spopov.drawio
