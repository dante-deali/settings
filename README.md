# 개발환경 설정

## max os x 개발환경 설정

### brew 설치 (필수)

[brew](https://brew.sh/index_ko) 는 mac os x 에서 각종 프로그램이나 개발도구들을 쉽게 설치할 수 있도록 도와주는 맥용 패키지 관리자입니다.
mac os x 를 사용하려면 거의 필수적으로 설치해야 하는 도구이므로 가장 먼저 `brew` 를 설치합니다.
`brew` 를 이용하지 않고 직접 홈페이지를 방문하여 설치 패키지를 다운로드 받아서 설치하는 경우도 가능합니다.
하지만, 향후 `uninstall` 또는 `update` 등을 고려해 본다고 할 때 `brew` 를 사용하는 것이 편리할 수 있습니다.

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

기존에는 mac os x 에 각종 개발도구를 설치하기 위해서는 의존적인 `gcc`, `make` 등을 설치하기 위해

```sh
xcode-select --install
```

을 통해 `명령어 도구` 를 설치해야 했으나, 이제는 `brew` 를 설치하면 자동으로 위의 명령을 수행하기 때문에 별도로 명령어 도구를 설치할 필요가 없습니다.

`brew` 의 설치가 완료되었다면

```sh
brew doctor
```

를 통해 설치가 정상적으로 이루어졌는지 확인하세요. (`Your system is ready to brew` 메시지가 보여지면 설치가 잘 된 것입니다.)

### git 및 git-lfs 설치 (필수)

`dealicious` 에서는 소스 형상관리 도구로 `github` 를 이용하고 있습니다. 따라서, `git` 도구를 설치해야 합니다.
`100MB` 이상의 대용량 `git repo` 를 포함(50MB 이상 시 warning 발생) 시키기 위해서 `git-lfs` 도 함께 설치 합니다.

```sh
brew install git git-lfs
```

git 설치가 완료되면 작업자 정보를 연동하고, 한글명을 제대로 표시하기 위해 추가 옵션을 지정합니다.

```sh
git config --global user.name "계정명"
git config --global user.email "이메일"
git config --global core.precomposeunicode true
git config --global core.quotepath false
```

### 터미널 설치 (옵션)

mac os x 에 기본적으로 설치된 `terminal app` 을 사용하시려면 이 부분은 넘어가셔도 됩니다.
mac os x 에서 작업하는 대부분의 개발자는 `terminal app` 대신 `iterm2` 를 이용하곤 합니다.
`terminal app` 역시 최근에는 상당히 좋아지고 있으나, 여전히 많은 개발자는 `iterm2` 에서 제공하는 [좋은 기능](https://iterm2.com/features.html)으로 인해 `iterm2` 를 선호하는 편입니다.

`iterm2` 역시 `brew` 를 통해 설치합니다.

```sh
brew install --cask iterm2
```

> `--cask` 옵션은 일반적으로 `brew` 에서 `gui` 도구를 설치할 용도로 사용하는 경우에 붙이는 옵션입니다. 원래는 독립적으로 개발되는 확장이었으나, 최근에는 core team 에서 거의 관리하고 있는 상태입니다. (brew search goland)

`iterm2 꾸미기` 로 검색하면 아주 많은 자료들을 찾을 수 있습니다. 본인이 원하거나 또는 본인이 익숙한 iterm2 설정을 하시면 됩니다.

### zsh with oh-my-zsh (필수)

mac os x `Catalina` 부터는 default shell 로 `zsh` 이 선택되었습니다. 예전부터, 개발자들은 주로 `bash` 대신 `oh-my-zsh` 을 연동한 `zsh` 을 즐겨 사용했습니다.
`bash` 와 `zsh` 간의 `뭐가 좋다` 라는 것은 많은 문서들에서 다루고 있지만, 사실이 아닌 경우도 많고 논쟁의 소지가 있습니다.
다만, 우리는 여기서 `oh-my-zsh` 이 주는 편리함으로 `prompt` 를 꾸미고, `명령구문을 강조` 하는 등의 여러가지 부가기능을 제공받기 위해 `oh-my-zsh` 을 통한 `zsh` 을 사용하는 것으로 하겠습니다.

`zsh` 을 최신으로 업데이트하고 `자동완성` 을 위한 [zsh-completions](https://github.com/zsh-users/zsh-completions) 을 설치합니다.

```sh
brew install zsh zsh-completions
```

이제 `zsh` 을 더욱 풍성하게 사용하기 위해 `oh-my-zsh` 을 설치합니다.

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

`oh-my-zsh` 까지 설치가 완료되었다면, 강력한 플러그인 설치를 통해 더욱 편리한 커맨드 라인 도구로 만들 필요가 있습니다. [command highligting](https://github.com/zsh-users/zsh-syntax-highlighting)(명령어의 존재여부에 따라 색상으로 구분할 수 있는 기능) 과 자동완성을 위한 [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) 을 설치합니다.

```sh
# zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

```sh
# zsh-autosuggestions
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

플러그인 설치 후 `iterm2` 나 `terminal` 이 실행될 때 마다 해당 플러그인을 활성화 해야 하기 때문에 아래와 같이 `~/.zshrc` 파일에 plugin 등록을 합니다.

```sh
plugins=(
  git
  zsh-syntax-highlighting
  zsh-autosuggestions
)
```

`~/.zshrc` 파일을 수정했다면 터미널을 재시작하거나 `source ~/zshrc` 명령으로 설정을 `reload` 합니다.

### 프롬프트 꾸미기

위에서 말한것과 같이 `oh-my-zsh` 에는 `프롬프트 꾸미기` 를 위한 장치가 잘 되어 있습니다. 각자가 선호하는 프롬프트의 형태가 있겠지만, 여기에서는 하나의 예시를 들고자 합니다.

`oh-my-zsh` 설치 이후 별도의 설정을 하지 않으면 `~/.zshrc` 파일 내에 `ZSH_THEME="robbyrussell"` 이라는 테마가 적용되어 있습니다. 이것을 [Powerlevel10K](https://github.com/romkatv/powerlevel10k) theme 로 변경해 보겠습니다.

`Powerlevel10K` 의 자세한 사용법은 [여기](https://github.com/romkatv/powerlevel10k) 에서 참고하세요.

우선, `Powerlevel10K` 를 설치합니다.

```sh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k
```

설치가 되었다면 `~/.zshrc` 파일 내에서 `ZSH_THEME` 항목을 수정합니다.

```sh
ZSH_THEME="powerlevel10k/powerlevel10k"
```

`~/.zshrc` 파일을 변경했으므로, 터미널을 재시작하거나 `source ~/zshrc` 명령으로 설정을 `reload` 합니다. 새롭게 시작하면 `powerlevel10k` 에서 제공하는 설정창을 볼 수 있습니다. 대화형으로 제공하는 설정과정을 모두 완료하면 본인의 취향에 맞는 터미널 프롬프트를 구성할 수 있습니다.

![https://raw.githubusercontent.com/romkatv/powerlevel10k-media/master/prompt-styles-high-contrast.png](https://raw.githubusercontent.com/romkatv/powerlevel10k-media/master/prompt-styles-high-contrast.png)

### 기타 환경설정

`프롬프트 꾸미기` 까지 진행했다면, 개발자스러운 환경을 구성했다고 볼 수 있습니다. 이제부터는 본인의 취향에 맞게 몇몇 도구들을 더 설치할 수 있습니다. 설치하면 도움이 될만한 도구들은 다음과 같습니다.

- 깔끔한 vi 구성하기 : [neovim](https://neovim.io/), [spacevim](https://spacevim.org/)
- 강력한 터미널 finder : [fzf](https://github.com/junegunn/fzf), [도움글](https://medium.com/harrythegreat/fzf%EB%A1%9C-zsh-%ED%84%B0%EB%AF%B8%EB%84%90-%EB%8D%94-%EA%B0%95%EB%A0%A5%ED%95%98%EA%B2%8C-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-730c20eb496b)
- 사용빈도가 높은 파일 및 디렉토리 검색 : [fasd](https://github.com/clvv/fasd), [도움글](https://ko.linux-console.net/?p=2085)

여기까지 기본 mac os x 꾸미기였습니다.

이제 `ruby` 및 `ruby on rails` 환경 구성을 진행해 보겠습니다. 아래 진행될 `ruby` 및 `ruby on rails` 환경 구성에 대한 부분은 `백엔드 개발팀 신규입사자` 에 해당하는 내용입니다. `프론트엔드 신규입사자` 는 패스해도 됩니다.

## Ruby on Rails 환경 구성하기

### rbenv 설치

본격적으로 `ruby on rails` 개발을 진행하기 위해 `ruby` 를 설치합니다. `ruby` 설치를 위해 `Homebrew` 를 이용합니다. `brew` 는 이미 위에서 설치를 했기 때문에 넘어가도 됩니다만, 아직 설치가 되어 있지 않다면 다음의 명령으로 `brew` 를 설치합니다.

```sh
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

이제 `brew` 를 이용하여 `ruby` 를 설치할 차례입니다. 원하는 `ruby` 버전을 직접 설치할 수 있지만, 여러 버전의 `ruby` 를 설치하고 관리하기 위해 [rbenv](https://github.com/rbenv/rbenv) 라고 하는 ruby version manager 를 통해 설치하도록 하겠습니다.
우선, `rbenv` 를 설치합니다.

```sh
brew install rbenv ruby-build
```

설치가 완료되면 `~/.zshrc` 파일에 rbenv 초기화 스크립트를 등록합니다.

```sh
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.zshrc
```

`~/.zshrc` 파일을 변경했으므로, 터미널을 재시작하거나 `source ~/zshrc` 명령으로 설정을 `reload` 합니다.

### ruby 설치

`rbenv` 가 설치되었으면 `rbenv` 를 통해 적당한 버전의 `ruby` 를 설치합니다. 여기에서는 `2.6.6` 으로 설치합니다.

```sh
# install ruby 2.6.6
rbenv install 2.6.6
rbenv global 2.6.6

# 설치 후 ruby version 확인
ruby -v

# ruby 2.6.6p146 (2020-03-31 revision 67876) [x86_64-darwin20]
# ruby 버전이 정상적으로 표시되지 않는다면 터미널을 재시작해 보세요.
```

### ruby on rails 프로젝트 생성 (옵션)

`python` 및 `nodejs` 진영에 `package` 라는 개념이 있다면, `ruby` 진영에서는 `gem` 이라는 개념이 존재합니다.
`rails` 역시 `gem` 이기 때문에 `ruby` 만 설치하였다면 `rails` 의 설치없이 `ruby on rails` 프로젝트를 시작할 수 있습니다.

```ruby
# Gemfile

source 'https://rubygems.org'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby '2.6.6'

gem 'rails', '~> 6.0.3', '>= 6.0.3.7'
```

위와 같이 `Gemfile` 을 만든 뒤 `bundle install` 을 수행하면 `rails 6.0.3.7` 버전을 다운로드 받습니다.

```sh
$ bundle install

Fetching gem metadata from https://rubygems.org/.............
Fetching gem metadata from https://rubygems.org/.
Resolving dependencies...
Using rake 13.0.3
Using concurrent-ruby 1.1.8
Using i18n 1.8.10
Using minitest 5.14.4
Using thread_safe 0.3.6
Using tzinfo 1.2.9
Using zeitwerk 2.4.2
Using activesupport 6.0.3.7
Using builder 3.2.4
Using erubi 1.10.0
Using mini_portile2 2.5.3
Using racc 1.5.2
Fetching nokogiri 1.11.7 (x86_64-darwin)
Installing nokogiri 1.11.7 (x86_64-darwin)
...
```

이제 `rails` 를 이용할 준비가 되었으니 아래와 같이 새로운 rails 기반 프로젝트를 생성합니다.

```sh
bundle exec rails new .

# frontend 를 react 와 연동하고 싶다면
# bundle exec rails new . --webpack=react
# 를 수행하면 됩니다.

# database 를 sqlite 가 아닌 mysql 로 설정하고 싶다면
# bundle exec rails new . --database=mysql
# 를 수행하면 됩니다.
```

아래와 같이 `Gemfile` 을 overrites 할 것이냐고 물어보면 `Y` 를 눌러줍니다.

```sh
exist
      create  README.md
      create  Rakefile
      create  .ruby-version
      create  config.ru
      create  .gitignore
    conflict  Gemfile
Overwrite /Users/dante/workspaces/newbie/backend/ruby_on_rails/temp/Gemfile? (enter "h" for help) [Ynaqdhm]
```

위와 같이 수행하면

![rails_new.png](https://st-kr-tutor.s3-ap-northeast-2.amazonaws.com/got/874982c46d3d120dfc7079bb4f9adf51/rails_new.png)

화면과 같이 초기 `rails project` 설정이 완료됩니다.
