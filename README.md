# 🔐 PAM 비밀번호 정책 설정

이 문서는 PAM(Pluggable Authentication Modules)을 사용하여 **비밀번호를 8자리 이상**으로 규제하는 방법을 설명합니다.

## ✨ 주요 기능

- 비밀번호의 최소 길이를 8자리로 규제
- PAM을 사용한 비밀번호 복잡성 강화
- 비밀번호 설정 테스트 및 확인 방법 제공

## ⚙️ 설정 방법

1. **PAM 설정 파일 편집**
   
   `pam_pwquality` 모듈을 사용하여 비밀번호 정책을 설정합니다. 다음 명령어를 사용하여 `/etc/pam.d/common-password` 파일을 엽니다.

   ```bash
   sudo nano /etc/pam.d/common-password
   ```

2. **비밀번호 최소 길이 설정**
   
   `pam_pwquality.so` 모듈을 사용하여 비밀번호의 최소 길이를 8자로 설정합니다. 다음 설정을 추가합니다:

   ```bash
   password requisite pam_pwquality.so retry=3 minlen=8
   ```

   - **retry=3**: 사용자가 비밀번호를 3번 시도할 수 있도록 허용
   - **minlen=8**: 비밀번호 최소 길이를 8자로 설정

3. **설정 저장 및 적용**

   파일을 저장하고 편집기를 종료합니다.

## 🧪 테스트 방법

1. **비밀번호 변경 시도**

   설정 후 사용자의 비밀번호를 변경하여 정책이 제대로 적용되는지 확인합니다:

   ```bash
   sudo addsuer user01
   sudo passwd user01
   ```

   8자리 미만의 비밀번호를 입력하면 오류 메시지가 표시되며, 규칙에 맞는 비밀번호를 입력해야만 변경이 가능합니다.

2. **로그 확인**

   비밀번호 정책 적용 후 문제가 발생할 경우, 다음 명령어로 시스템 로그를 확인할 수 있습니다:

   ```bash
   sudo tail -f /var/log/auth.log
   ```

