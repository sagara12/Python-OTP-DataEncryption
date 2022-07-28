# OTP기능 및 DB 정보 암호화
## 기능 구현
* OTP 로그인 기능 구현
* 확인 문자 전송 기능
* QR 코드를 통한 구글 OTP 연결
* txt파일에 기록된 DB 정보 암호화

## 참고 사이트

* https://blog.naver.com/chandong83/221966470981 ->  OTP 구현 (Python)
* https://zero-gravity.tistory.com/221 -> Googl OTP 구현 (JAVA)
* https://thinkingfactory.tistory.com/989 -> Twilo를 이용해서 문자 보내기 기능 (Python)
* https://gdbs.tistory.com/498 -> URL을 QR 코드로 변환
* https://appia.tistory.com/353 -> 필로우를 통한 png 출력

## 코드 구현
```Python
from cryptography.fernet import Fernet # symmetric encryption

class DbdataDecryption():

    def __init__(self, key=None):
        if key is None:  # 키가 없다면
            key = b'zCJqo_kdutX3uSmz9iso8-4XBABGROF3T2-DRaZ7Re0='  # 키를 생성한다
        self.key = key
        self.f = Fernet(self.key)

    def encrypt(self, data, is_out_string=True):
        if isinstance(data, bytes):
            ou = self.f.encrypt(data)  # 바이트형태이면 바로 암호화
        else:
            ou = self.f.encrypt(data.encode( encoding="utf-8"))  # 인코딩 후 암호화
        if is_out_string is True:
            return ou.decode('utf-8')  # 출력이 문자열이면 디코딩 후 반환
        else:
            return ou

    def decrypt(self, data, is_out_string=True):
        if isinstance(data, bytes):
            ou = self.f.decrypt(data)  # 바이트형태이면 바로 복호화
        else:
            ou = self.f.decrypt(data.encode('utf-8'))  # 인코딩 후 복호화
        if is_out_string is True:
            return ou.decode('utf-8')  # 출력이 문자열이면 디코딩 후 반환
        else:
            return 
```
