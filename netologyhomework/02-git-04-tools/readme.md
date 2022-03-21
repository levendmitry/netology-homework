1 Ищем коммит по хэшу.  
  Полный хэш: "aefead2207ef7e2aa5dc81a34aedf0cad4c32545"  
  Комментарий: "Update CHANGELOG.md"
  

    $ git log aefea
    commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545
    Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
    Date:   Thu Jun 18 10:29:58 2020 -0400
    Update CHANGELOG.md  
2 Ищем коммит по хэшу.  
  Тэг: "v0.12.23"

    $ git log 85024d3
    commit 85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23)
    Author: tf-release-bot <terraform@hashicorp.com>
    Date:   Thu Mar 5 20:56:10 2020 +000  
3 Ищем коммит по хэшу и в формате вывода просим вывести полный хэш коммита и полные хэши предков.  
  Два родителя:  
  56cd7859e05c36c06b56d013b55a252d0bb7e158  
  9ea88f22fc6269854151c571162c5bcf958bee2b

    $ git log b8d720 --pretty=oneline --pretty=format:"%H"--"%P" --graph  
  
4 Ищем коммит по тэгам, получаем коммиты в нужном диапазоне.
  
    $ git log --pretty=oneline v0.12.23..v0.12.24
    
    33ff1c03bb960b332be3af2e333462dde88b279e (tag: v0.12.24) v0.12.24
    b14b74c4939dcab573326f4e3ee2a62e23e12f89 [Website] vmc provider links
    3f235065b9347a758efadc92295b540ee0a5e26e Update CHANGELOG.md
    6ae64e247b332925b872447e9ce869657281c2bf registry: Fix panic when server is unreachable
    5c619ca1baf2e21a155fcdb4c264cc9e24a2a353 website: Remove links to the getting started guide's old location
    06275647e2b53d97d4f0a19a0fec11f6d69820b5 Update CHANGELOG.md
    d5f9411f5108260320064349b757f55c09bc4b80 command: Fix bug when using terraform login on Windows
    4b6d06cc5dcb78af637bbb19c198faff37a066ed Update CHANGELOG.md
    dd01a35078f040ca984cdd349f18d0b67e486c35 Update CHANGELOG.md
    225466bc3e5f35baa5d07197bbc079345b77525e Cleanup after v0.12.23 release
  
  
5 Ищем коммит по строчке в файле.  
  commit 8c928e83589d90a031f811fae52a81be7153e82f  

    $ git log -Sfunc\ providerSource\(  
  
6 Находим имя файла с функцией, затем ищем все комиты, которые связанны с файлом  
  commit 78b12205587fe839f10d946ea3fdc06719decb05  
  commit 52dbf94834cb970b510f2fba853a5b49ad9b1a46  
  commit 41ab0aef7a0fe030e84018973a64135b11abcd70  
  commit 66ebff90cdfaa6938f26f908c7ebad8d547fea17  
  commit 8364383c359a6b738a436d1b7745ccdce178df47  

    $ git grep -p globalPluginDirs  
    $ git log -L :globalPluginDirs:plugins.go

7 Ищем коммиты по строке в файле. Автор саммого раннего коммита и является автором функции.  
  Автор: "Martin Atkins"

    $ git log -SsynchronizedWriters --pretty=format:'%h | %an | %aD'
    bdfea50cc | James Bardin | Mon, 30 Nov 2020 18:02:04 -0500
    fd4f7eb0b | James Bardin | Wed, 21 Oct 2020 13:06:23 -0400
    5ac311e2a | Martin Atkins | Wed, 3 May 2017 16:25:41 -0700
