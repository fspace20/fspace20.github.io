# [F:SPACE](http://fspace20.github.io)
So Simple themed Gitblog

---

## Git Setting 

### SSH Setting for Mutliple Git IDs
+ SSH 키 생성
  ```
  cd ~/.ssh/
  ssh-keygen -t rsa -C "e_idA@email.com" -f "id_rsa_gitidA"
  ssh-keygen -t rsa -C "e_idB@email.com" -f "id_rsa_gitidB"
  ```
  - 계정별 이메일 확인: [Github Settings > Emails](https://github.com/settings/emails)
+ SSH 키 등록
  - Local
    ```
    ssh-add id_rsa_gitidA
	  ssh-add id_rsa_gitidB
    ```
  - Github
    * SSH 공개키 출력
    ```
    cat ~/.ssh/id_rsa_gitidA.pub
	  cat ~/.ssh/id_rsa_gitidB.pub
    ```
    * SSH 공개키 추가  
      : [Github Settings > SSH and GPG keys > New SSH Key](https://github.com/settings/keys)
+ SSH 키 설정파일
  - 설정파일 생성/수정
    ```
    sudo nano ~/.ssh/config
    ```
  - 수정예시
    ```
    # Git SSH account-idA (unnecessary comment)
    Host github.com-gitidA
		HostName github.com
		User git
        	IdentityFile ~/.ssh/id_rsa_gitidA

    # Git SSH account-idB
    Host github.com-gitidB
		HostName github.com
		User git
        	IdentityFile ~/.ssh/id_rsa_gitidB
    ```
+ 참조: [한 컴퓨터에서 여러 개의 깃허브 계정 사용하기](https://velog.io/@jay/multiplegithubaccounts)

### Git Local Config
+ Git 로컬설정 확인
  ```
  cd my_projA
  git init
  git config --list
  ```
+ Git user 설정
  ```
  git config user.name gitidA
  git config user.email e_idA@email.com
  ```
+ Git origin 설정  
  : `~/.ssh/config` 파일의 Host 설정값 반영 *ex) github.com-gitidA*
  - 추가
    ```
    git remote add origin git@github.com-gitidA:gitidA/myprojectA.git
    ```  
  - 수정
    ```
    git remote set-url origin git@github.com-gitidA:gitidA/myprojectA.git
    ```

---

## Installation (MacOS)

### Setting Ruby (rbenv)
+ 설치
  - brew 이용 설치
    ```
    # install Homebrew
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    # install rbenv
    brew updates
    brew install rbenv
    brew upgrade ruby-build
    ```
  - ruby 지원 버전 확인 및 설치
    ```
    rbenv install -l
    rbenv install 2.7.2
    rbenv rehash
    ```
+ 연동
  - rbenv 적용 및 설치확인
    ```
    rbenv init
    curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/ rbenv-doctor | bash
    ```
  - rbenv 연동 및 경로설정  
    : ` ~/.bash_profile` 파일에 설정 추가  
    ```
    # rbenv auto load
    eval "$(rbenv init -)"

    # gem env added (version: X.X.Y -> X.X.0)
    export PATH="$HOME/.gem/ruby/2.7.0/bin:$PATH"
    ```
  - 터미널 재시작 및 연동된 ruby 버전 확인
    ```
    ruby -v
    ```
+ 참조
  - [초레가 rbenv 설치](https://www.railsguidebook.com/contents/rbenv.html)
  - [MacOS에 Jekyll 설치](http://jekyllrb-ko.github.io/docs/installation/macos/)

### Setting Jekyll
+ jekyll & bundler 설치
  ```
  gem install jekyll bundler
  bundle update
  ```
+ jekyll 프로젝트 생성 
  ```
  jekyll new myblog
  ```
+ So-Simple Theme 적용
  - `_config.yml` 파일 수정
    ```
    theme: jekyll-theme-so-simple
    ```
  - `Gemfile` 파일에 추가
    ```
    gem "jekyll-theme-so-simple"
    ```
+ 적용 및 테스트
  ```
  bundle install
  bundle exec jekyll serve
  ```
