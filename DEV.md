# DEV.md

# 1. mac 개발환경셋팅
## 1-1. Homebrew 설치
```
# homebrew 설치 확인
brew --version

# homebrew 설치 (https://brew.sh)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## 1-2. rbenv 설치
- Mac에는 Ruby가 기본적으로 설치되어 있지만 우리는 React Native에서 필요한 Ruby 버전을 설치해야 한다. 
```
# rbenv 설치
brew install rbenv

# 필요한 버전 설치
rbenv install 2.7.6

# 설치한 버전을 기본 버전으로 설정
rbenv global 2.7.6
rbenv rehash

# Ruby bundler 설치
gem install bundler

# gem install bundler 명령어 실행 시 permissions 에러가 나는 경우
1. vi ~/.zshrc
2. 아래 코드 추가 후 저장
[[ -d ~/.rbenv  ]] && \
  export PATH=${HOME}/.rbenv/bin:${PATH} && \
  eval "$(rbenv init -)"
3. source ~/.zshrc
4. gem install bundler 명령어 다시 실행
```

## 1-3. Nodejs 설치
```
# node 설치 확인
node -v
npm -v

# node 설치
brew install node
```

## 1-4. Xcode 설치
- 앱스토어에서 설치하면 된다.

## 1-5. Cocoapods 설치
```
# pod 설치 확인
pod --version

# pod 설치
sudo gem install cocoapods
```

## 1-6. Watchman 설치
```
# watchman 설치 확인
watchman -v

# watchman 설치
brew install watchman
```

## 1-7. JDK 설치
```
# 확인
java -version
javac -version

# AdoptOpenJDK/openjdk 이름의 패키지 저장소를 추가
brew tap AdoptOpenJDK/openjdk

# 명령어를 입력하면 설치할 수 있는 jdk 목록을 보여준다.
brew search jdk

# openjdk설치, --cask 뒤에 원하는 버전을 입력한다.
brew install --cask adoptopenjdk11
```

## 1-8. 안드로이드 스튜디오 설치
- 안드로이드 스튜디오 사이트에서 설치하면 된다. <https://developer.android.com/studio>
- 설치 후 설정이 필요함.
  - SDK Manager 에서 다음 항목 설치
    - Android SDK Platform 29
    - Intel x86 Atom System Image
    - Google APIs Intel x86 Atom System Image
    - Google APIs Intel x86 Atom_64 System Image 
  - 안드로이드 환경변수 설정
    ```
    1. vi ~/.zshrc
    2. 아래 코드 추가 후 저장 // [안드로이드SDK위치]는 안드로이드 스튜디오 SDK Manager에서 확인 가능함.
    export ANDROID_HOME=[안드로이드SDK위치]/Android/sdk
    export PATH=$PATH:$ANDROID_HOME/emulator
    export PATH=$PATH:$ANDROID_HOME/tools
    export PATH=$PATH:$ANDROID_HOME/tools/bin
    export PATH=$PATH:$ANDROID_HOME/platform-tools
    3. source ~/.zshrc
    4. adb // 완료됐는지 확인
    ```

## 1-9. React-Native 프로젝트 생성
- 프로젝트 생성이 잘 되는지 확인
- RN공식문서에서 react-native-cli를 삭제하고 npx를 사용하라고 함.
```
# reacet-native-cli가 글로벌로 설치되어있으면 삭제해야함.
npm uninstall -g react-native-cli @react-native-community/cli

# 프로젝트를 생성할 위치에서 프로젝트 생성
npx react-native init rn_test

# 타입스크립트로 생성하려면 아래 명령어 실행
npx react-native init rn_test_ts --template react-native-template-typescript

#프로젝트로 이동
cd rn_test

# 프로젝트 실행
yarn start

# 안드로이드 실행
yarn start 동작중인 터미널에서 a 입력
OR
yarn android

# ios 실행
yarn start 동작중인 터미널에서 a 입력
OR
yarn ios

# ios 실행 에러 시
1. cd ios
2. pod install
3. cd ..
4. yarn ios
```

## 참고
- <https://myung-ho.tistory.com/116>

<br/>

# 2. window 개발환경셋팅

<br/>

# 3. Build
## 3-1. Android
- Debug 
  - android/app/src/main에 assets 폴더 만들기 
  - npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res/
  - cd android
  - ./gradlew clean  // build cache 지우는 명령어
  - ./gradlew assembleDebug  // Debug 용 apk 파일 생성
  - android/app/build/outputs/apk/debug 경로에서 app-debug.apk 파일 확인
  - 참고
    - <https://velog.io/@ioijhioi/React-native-.apk%ED%8C%8C%EC%9D%BC-%EC%B6%94%EC%B6%9C%ED%95%98%EA%B8%B0>
      
- Release
  - cd android
  - ./gradlew clean
  - ./gradlew assembleRelease  // Release 용 apk 파일 생성
  - android/app/build/outputs/apk/release 경로에서 app-release.apk 파일 확인
  - ./gradlew bundleRelease  // Release 용 aab 파일 생성
  - android/app/build/outputs/bundle/release 경로에서 app-release.aab 파일 확인
  - 참고
    - <https://ssilook.tistory.com/entry/React-Native-RN-APK-%EC%B6%94%EC%B6%9C%ED%95%98%EA%B8%B0-3%ED%8E%B8AAB-%ED%8C%8C%EC%9D%BC-%EC%83%9D%EC%84%B1>

## 3-2. ios
  - xcode
