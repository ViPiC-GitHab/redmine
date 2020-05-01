# ��������
`JScript` ��� �������������� � [Redmine](http://www.redmine.org/) �� ��������� `REST API` � `WSH` ����� ������������ ������� **Windows**. � ������ ������� ������ ������������ ��� ������������� � ������������ �����. � ������� ������� ����� ������������ ������������� ������������� � **Active Directory** ����� `LDAP` � �������������� ��������� (��������) �����. ��� �������������� � **Redmine** ������������ `XML` ������.
# �������������
� ��������� ������ **Windows** ������� ��������� �������:
```bat
cscript redmine.min.js <url> <key> <method> [... <param>]
```
- `<url>` - ������� url ����� ��� �������� � **REST API**. ����� ����� � ����� �� �����������. �������� ������ � ������ ��� **Basic Authentication** �� ��������������.
- `<key>` - ���� ������� � **REST API** ��� ��������������. ��� �������� **REST API** � ���������� ���� ������������ ��� �������������� ������� � [����������� ������������](http://www.redmine.org/projects/redmine/wiki/Rest_api).
- `<method>` - ��� ������������ ����� ������� ����� ���������.
- ... `<param>` - ��������� ��� ������.
## ����������� ������
`users.sync` - ������������� ������������� � **Active Directory** ����� **LDAP**. ����� ��������� ������ � ������������� **Redmine**, �������� ����������� ������������� � �������� �����. ������������ **Redmine**, � ������� ��� ��������������� ������������� � ���������� **Active Directory**, �� ���������. ������������ ����������� �� ������ ������������. ����������� � **Active Directory** ��� � ��������� �������� ������������, ������� ��� ������� ������� �� ������������ ����� �� �������� ������� �� ����� ������ ������������ ��������� ������.
```bat
cscript redmine.min.js <url> <key> users.sync <fields> [<container>] [<auth>]
```
- `<fields>` - ������������ **��������������** ���� ������������ � ��� �������� � ������� `id:value;id:value` � ���������� ������������ **������** ��������� **LDAP**. ��� **������������� �����** ������������� ������� ������������� ���� � ���� �����.
- `<container>` - ��������� � ������� ������ ������������� � **Active Directory**. ����� ������� **GUID**, **name**, **distinguishedName**, **sAMAccountName** ��� **LDAP-SQL** ������ � ������������� � ����������� `{select}`, `{protocol}`, `{parent}`. � �������� **LDAP-SQL** ������� ����� ������� ����� ������� ������� � `WHERE`.
- `<auth>` - ������������� ������ �������������� � ����������. �������������� ����� ���������� �� �������� **������ ��������������** *(����������������� - ����������� � ������� LDAP)* � **Redmine**.

`issues.change` - ��������� �����. ����� �������� ������ � �������� �����. �������������� �������������� ����������.
```bat
cscript redmine.min.js <url> <key> issues.change [<query>] <fields> [<filters>]
```
- `<query>` - ������������� ������������ ������� ��� ���� ��������. ������� ����� �������� �� �������� **������** � **Redmine**. ������� ��������� � ������ ����� � ����������� **����������� �������** � **��� ����������� �������**. ������ ������ ���� ����� ��-��� ������������ ���� ������� �������� ������������ ��� �������������� � **REST API**. � ���������� ������� ����������� ������ ������ ������� **��� ���� ��������**.
- `<fields>` - ���� � �� �������� � ������� `id:value;id:value` � ���������� ������������. ���� � �������� ���� ���������� �������, �� ��� �������� ����� ��������� � ������� �������. ��� **������������� �����** ������ ������� ������������� ���� � ���� �����.
- `<filters>` - �������������� ������ ��� ����� � ������� `id:value;id:value` � ���������� ������������. ���� � �������� ���� ���������� �������, �� ��� �������� ����� ��������� � ������� �������.
## ������������
� **����������** � **���������**, ������� ������������ ������������, ����� ��������� �������. **������** �� ���� ������������ ������ ������� ����� ��������� *(� ����� � �� ���������)* ���� ��� ��������� ������������ `|`. **�����������** ����� ������ �� ���������. � **���������** ������ ����� ����������� *(� ����� � �� �����������)* ���� ��� ��������� ���������� �� ��������. **���������** �� �������� `{object.key.id>filter}` ������������ �� ���� ������������������ ������ �� ������� ����� ������ � ������� ����� �������� ��������. ���� **��������** �����������, �� **��������** ��������� *(��� �������� ��������� �������� ������ ������ �������������, � �� ���� ������)*. � �������� **�������** ������������ �������� � ������� �������� ������. ���� ����� �������� �������� �����������, �� ��������� ����������� ��������� ��� ������.
```
"����� ��� �������|| {author.name} ������� {project.name>clear}| {done} %|."
```
� **����������** �� �������� ����� ��������� ������������������ **�������** ��� ��������� ��������. ��������������� ��������� �������:
- `hash` - ��������� ������ ����� �������� ������� ��� ����� ������� `#`.
- `phone` - �������� �������� ��� ���������� ����� � ������� `+X (XXX) XXX-XX-XX`.
- `user`, `issue`, `project` - �������� �� �������� ��������������� ������ ��� �������� ��� ��������.
- `clear` - ������ ������ ������ ��������� � ������� ����� � �����, ���� ��� �����������. ��� �� ������� `FW:` � `RE:` � ������ ��������.
# ������� �������������
���������������� ������������� �� ���������� **Active Directory** � **GUID** `{8F640E75-C072-47CA-5DBD-66AFC5D7E38F}` � ���������� **Redmine** ������������� �� ������ https://redmine.org ��������� **���� �������** ������������ `8dbfd7b0a9c9279a97fedfb82710aed96bcf53fc`. � **������������� �����** � ��������������� **12** �������� **������� ������������** ������������. ������� **����� ��������������** ��� **1**.
```bat
cscript redmine.min.js https://redmine.org 8dbfd7b0a9c9279a97fedfb82710aed96bcf53fc users.sync
login:{sAMAccountName};firstname:{givenName};lastname:{sn};mail:{mail};12:"{manager.sAMAccountName>user.lastname}"
{8F640E75-C072-47CA-5DBD-66AFC5D7E38F} 1
```
�������� ������������� **�������** �� **8**, ������� **����������** �� **10** � �������� **�����������** � ������������� ��� ����� �� **������������ �������** � ��������������� **46**, ���� **��������** ������ �������� `������`, **������������� ����** � ��������������� **10** �������� `�����`, ��� **�� ���������** ������ � ������ ��������� ������.
```bat
cscript redmine.min.js https://redmine.org 8dbfd7b0a9c9279a97fedfb82710aed96bcf53fc issues.change
46 status:8;done:10;notes:"{author.name}, ���� ������ ������������� ���������������� � �������."
description:������;10:�����;private:true;assigned.id:{author.id}
```