# [GUIDES](../../../../../README.md) -> [MarkDown](MarkDown.md) -> __Languages known to GitHub (c)__

## __List of Guides__

| Guide Name                    |   |  Guide Name                   |   | Guide Name                    |
|-------------------------------|---|-------------------------------|---|-------------------------------|
| [Windows][navWin]             | * | [Linux][navNix]               | * | [Networks][navNet]            |
| [Databases][navDBs]           | * | [Programming][navPLn]         | * | [Git & GitHub][navGit]        |
| [CMake][navCMk]               | * | [Docker & Kubernetes][navDkr] | * | [Embedded systems][navEmS]    |

[navWin]:   ../../../../002_Windows_/Windows.md
[navNix]:   ../../../../003_Linux_(Unix)_/Linux_(Unix).md
[navNet]:   ../../../../004_Networks_/Networks.md
[navDBs]:   ../../../../006_Databases_/Databases.md
[navPLn]:   ../../../../005_Programming_languages_/Programming.md
[navGit]:   ../../../../001_Git_and_GitHub_/Git_And_GitHub.md
[navCMk]:   ../../../../009_CMake_/CMake_Tutorial.md
[navDkr]:   ../../../../007_Docker_and_Kubernetes_/Docker_and_Kubernates.md
[navEmS]:   ../../../../008_Embedded_systems_/Embedded_systems.md

---
<!-- ---------------------------------- * Navigation * ---------------------------------- -->

- [GUIDES -\> MarkDown -\> __Languages known to GitHub (c)__](#guides---markdown---languages-known-to-github-c)
  - [__List of Guides__](#list-of-guides)
  - [__C__](#c)
  - [__C#__](#c-1)
  - [__C++__](#c-2)
  - [__C-ObjDump__](#c-objdump)
  - [__C2hs Haskell__](#c2hs-haskell)
  - [__Cabal Config__](#cabal-config)
  - [__Cap'n Proto__](#capn-proto)
  - [__CartoCSS__](#cartocss)
  - [__Ceylon__](#ceylon)
  - [__Chapel__](#chapel)
  - [__Charity__](#charity)
  - [__ChucK__](#chuck)
  - [__CIL__](#cil)
  - [__Cirru__](#cirru)
  - [__Clarion__](#clarion)
  - [__Classic ASP__](#classic-asp)
  - [__Clean__](#clean)
  - [__Click__](#click)
  - [__CLIPS__](#clips)
  - [__Clojure__](#clojure)
  - [__Closure Templates__](#closure-templates)
  - [__Cloud Firestore Security Rules__](#cloud-firestore-security-rules)
  - [__CMake__](#cmake)
  - [__COBOL__](#cobol)
  - [__CODEOWNERS__](#codeowners)
  - [__CodeQL__](#codeql)
  - [__CoffeeScript__](#coffeescript)
  - [__ColdFusion__](#coldfusion)
  - [__ColdFusion CFC__](#coldfusion-cfc)
  - [__COLLADA__](#collada)
  - [__Common Lisp__](#common-lisp)
  - [__Common Workflow Language__](#common-workflow-language)
  - [__Component Pascal__](#component-pascal)
  - [__CoNLL-U__](#conll-u)
  - [__Cool__](#cool)
  - [__Coq__](#coq)
  - [__Cpp-ObjDump__](#cpp-objdump)
  - [__Creole__](#creole)
  - [__Crystal__](#crystal)
  - [__CSON__](#cson)
  - [__Csound__](#csound)
  - [__Csound Document__](#csound-document)
  - [__Csound Score__](#csound-score)
  - [__CSS__](#css)
  - [__CSV__](#csv)
  - [__Cuda__](#cuda)
  - [__CUE__](#cue)
  - [__Cue Sheet__](#cue-sheet)
  - [__cURL Config__](#curl-config)
  - [__CWeb__](#cweb)
  - [__Cycript__](#cycript)
  - [__Cython__](#cython)

## __C__

```yml
%YAML 1.2
---
C:
  type: programming
  color: "#555555"
  extensions:
  - ".c"
  - ".cats"
  - ".h"
  - ".idc"
  interpreters:
  - tcc
  tm_scope: source.c
  ace_mode: c_cpp
  codemirror_mode: clike
  codemirror_mime_type: text/x-csrc
  language_id: 41
```

## __C#__

```yml
%YAML 1.2
---
C#:
  type: programming
  ace_mode: csharp
  codemirror_mode: clike
  codemirror_mime_type: text/x-csharp
  tm_scope: source.cs
  color: "#178600"
  aliases:
  - csharp
  - cake
  - cakescript
  extensions:
  - ".cs"
  - ".cake"
  - ".csx"
  - ".linq"
  language_id: 42
```

## __C++__

```yml
%YAML 1.2
---
C++:
  type: programming
  tm_scope: source.c++
  ace_mode: c_cpp
  codemirror_mode: clike
  codemirror_mime_type: text/x-c++src
  color: "#f34b7d"
  aliases:
  - cpp
  extensions:
  - ".cpp"
  - ".c++"
  - ".cc"
  - ".cp"
  - ".cxx"
  - ".h"
  - ".h++"
  - ".hh"
  - ".hpp"
  - ".hxx"
  - ".inc"
  - ".inl"
  - ".ino"
  - ".ipp"
  - ".re"
  - ".tcc"
  - ".tpp"
  language_id: 43
```

## __C-ObjDump__

```yml
%YAML 1.2
---
C-ObjDump:
  type: data
  extensions:
  - ".c-objdump"
  tm_scope: objdump.x86asm
  ace_mode: assembly_x86
  language_id: 44
```

## __C2hs Haskell__

```yml
%YAML 1.2
---
C2hs Haskell:
  type: programming
  group: Haskell
  aliases:
  - c2hs
  extensions:
  - ".chs"
  tm_scope: source.haskell
  ace_mode: haskell
  codemirror_mode: haskell
  codemirror_mime_type: text/x-haskell
  language_id: 45
```

## __Cabal Config__

```yml
%YAML 1.2
---
Cabal Config:
  type: data
  color: "#483465"
  aliases:
  - Cabal
  extensions:
  - ".cabal"
  filenames:
  - cabal.config
  - cabal.project
  ace_mode: haskell
  codemirror_mode: haskell
  codemirror_mime_type: text/x-haskell
  tm_scope: source.cabal
  language_id: 677095381
```

## __Cap'n Proto__

```yml
%YAML 1.2
---
Cap'n Proto:
  type: programming
  color: "#c42727"
  tm_scope: source.capnp
  extensions:
  - ".capnp"
  ace_mode: text
  language_id: 52
```

## __CartoCSS__

```yml
%YAML 1.2
---
CartoCSS:
  type: programming
  aliases:
  - Carto
  extensions:
  - ".mss"
  ace_mode: text
  tm_scope: source.css.mss
  language_id: 53
```

## __Ceylon__

```yml
%YAML 1.2
---
Ceylon:
  type: programming
  color: "#dfa535"
  extensions:
  - ".ceylon"
  tm_scope: source.ceylon
  ace_mode: text
  language_id: 54
```

## __Chapel__

```yml
%YAML 1.2
---
Chapel:
  type: programming
  color: "#8dc63f"
  aliases:
  - chpl
  extensions:
  - ".chpl"
  tm_scope: source.chapel
  ace_mode: text
  language_id: 55
```

## __Charity__

```yml
%YAML 1.2
---
Charity:
  type: programming
  extensions:
  - ".ch"
  tm_scope: none
  ace_mode: text
  language_id: 56
```

## __ChucK__

```yml
%YAML 1.2
---
ChucK:
  type: programming
  color: "#3f8000"
  extensions:
  - ".ck"
  tm_scope: source.java
  ace_mode: java
  codemirror_mode: clike
  codemirror_mime_type: text/x-java
  language_id: 57
```

## __CIL__

```yml
%YAML 1.2
---
CIL:
  type: data
  tm_scope: source.cil
  extensions:
  - ".cil"
  ace_mode: text
  language_id: 29176339
```

## __Cirru__

```yml
%YAML 1.2
---
Cirru:
  type: programming
  color: "#ccccff"
  tm_scope: source.cirru
  ace_mode: cirru
  extensions:
  - ".cirru"
  language_id: 58
```

## __Clarion__

```yml
%YAML 1.2
---
Clarion:
  type: programming
  color: "#db901e"
  ace_mode: text
  extensions:
  - ".clw"
  tm_scope: source.clarion
  language_id: 59
```

## __Classic ASP__

```yml
%YAML 1.2
---
Classic ASP:
  type: programming
  color: "#6a40fd"
  tm_scope: text.html.asp
  aliases:
  - asp
  extensions:
  - ".asp"
  ace_mode: text
  language_id: 8
```

## __Clean__

```yml
%YAML 1.2
---
Clean:
  type: programming
  color: "#3F85AF"
  extensions:
  - ".icl"
  - ".dcl"
  tm_scope: source.clean
  ace_mode: text
  language_id: 60
```

## __Click__

```yml
%YAML 1.2
---
Click:
  type: programming
  color: "#E4E6F3"
  extensions:
  - ".click"
  tm_scope: source.click
  ace_mode: text
  language_id: 61
```

## __CLIPS__

```yml
%YAML 1.2
---
CLIPS:
  type: programming
  color: "#00A300"
  extensions:
  - ".clp"
  tm_scope: source.clips
  ace_mode: text
  language_id: 46
```

## __Clojure__

```yml
%YAML 1.2
---
Clojure:
  type: programming
  tm_scope: source.clojure
  ace_mode: clojure
  codemirror_mode: clojure
  codemirror_mime_type: text/x-clojure
  color: "#db5855"
  extensions:
  - ".clj"
  - ".boot"
  - ".cl2"
  - ".cljc"
  - ".cljs"
  - ".cljs.hl"
  - ".cljscm"
  - ".cljx"
  - ".hic"
  filenames:
  - riemann.config
  language_id: 62
```

## __Closure Templates__

```yml
%YAML 1.2
---
Closure Templates:
  type: markup
  color: "#0d948f"
  ace_mode: soy_template
  codemirror_mode: soy
  codemirror_mime_type: text/x-soy
  aliases:
  - soy
  extensions:
  - ".soy"
  tm_scope: text.html.soy
  language_id: 357046146
```

## __Cloud Firestore Security Rules__

```yml
%YAML 1.2
---
Cloud Firestore Security Rules:
  type: data
  color: "#FFA000"
  ace_mode: less
  codemirror_mode: css
  codemirror_mime_type: text/css
  tm_scope: source.firestore
  filenames:
  - firestore.rules
  language_id: 407996372
```

## __CMake__

```yml
%YAML 1.2
---
CMake:
  type: programming
  color: "#DA3434"
  extensions:
  - ".cmake"
  - ".cmake.in"
  filenames:
  - CMakeLists.txt
  tm_scope: source.cmake
  ace_mode: text
  codemirror_mode: cmake
  codemirror_mime_type: text/x-cmake
  language_id: 47
```

## __COBOL__

```yml
%YAML 1.2
---
COBOL:
  type: programming
  extensions:
  - ".cob"
  - ".cbl"
  - ".ccp"
  - ".cobol"
  - ".cpy"
  tm_scope: source.cobol
  ace_mode: cobol
  codemirror_mode: cobol
  codemirror_mime_type: text/x-cobol
  language_id: 48
```

## __CODEOWNERS__

```yml
%YAML 1.2
---
CODEOWNERS:
  type: data
  filenames:
  - CODEOWNERS
  tm_scope: text.codeowners
  ace_mode: gitignore
  language_id: 321684729
```

## __CodeQL__

```yml
%YAML 1.2
---
CodeQL:
  type: programming
  color: "#140f46"
  extensions:
  - ".ql"
  - ".qll"
  tm_scope: source.ql
  ace_mode: text
  language_id: 424259634
  aliases:
  - ql
```

## __CoffeeScript__

```yml
%YAML 1.2
---
CoffeeScript:
  type: programming
  tm_scope: source.coffee
  ace_mode: coffee
  codemirror_mode: coffeescript
  codemirror_mime_type: text/x-coffeescript
  color: "#244776"
  aliases:
  - coffee
  - coffee-script
  extensions:
  - ".coffee"
  - "._coffee"
  - ".cake"
  - ".cjsx"
  - ".iced"
  filenames:
  - Cakefile
  interpreters:
  - coffee
  language_id: 63
```

## __ColdFusion__

```yml
%YAML 1.2
---
ColdFusion:
  type: programming
  ace_mode: coldfusion
  color: "#ed2cd6"
  aliases:
  - cfm
  - cfml
  - coldfusion html
  extensions:
  - ".cfm"
  - ".cfml"
  tm_scope: text.html.cfm
  language_id: 64
```

## __ColdFusion CFC__

```yml
%YAML 1.2
---
ColdFusion CFC:
  type: programming
  color: "#ed2cd6"
  group: ColdFusion
  ace_mode: coldfusion
  aliases:
  - cfc
  extensions:
  - ".cfc"
  tm_scope: source.cfscript
  language_id: 65
```

## __COLLADA__

```yml
%YAML 1.2
---
COLLADA:
  type: data
  color: "#F1A42B"
  extensions:
  - ".dae"
  tm_scope: text.xml
  ace_mode: xml
  codemirror_mode: xml
  codemirror_mime_type: text/xml
  language_id: 49
```

## __Common Lisp__

```yml
%YAML 1.2
---
Common Lisp:
  type: programming
  tm_scope: source.lisp
  color: "#3fb68b"
  aliases:
  - lisp
  extensions:
  - ".lisp"
  - ".asd"
  - ".cl"
  - ".l"
  - ".lsp"
  - ".ny"
  - ".podsl"
  - ".sexp"
  interpreters:
  - lisp
  - sbcl
  - ccl
  - clisp
  - ecl
  ace_mode: lisp
  codemirror_mode: commonlisp
  codemirror_mime_type: text/x-common-lisp
  language_id: 66
```

## __Common Workflow Language__

```yml
%YAML 1.2
---
Common Workflow Language:
  aliases:
  - cwl
  type: programming
  ace_mode: yaml
  codemirror_mode: yaml
  codemirror_mime_type: text/x-yaml
  extensions:
  - ".cwl"
  interpreters:
  - cwl-runner
  color: "#B5314C"
  tm_scope: source.cwl
  language_id: 988547172
```

## __Component Pascal__

```yml
%YAML 1.2
---
Component Pascal:
  type: programming
  color: "#B0CE4E"
  extensions:
  - ".cp"
  - ".cps"
  tm_scope: source.pascal
  ace_mode: pascal
  codemirror_mode: pascal
  codemirror_mime_type: text/x-pascal
  language_id: 67
```

## __CoNLL-U__

```yml
%YAML 1.2
---
CoNLL-U:
  type: data
  extensions:
  - ".conllu"
  - ".conll"
  tm_scope: text.conllu
  ace_mode: text
  aliases:
  - CoNLL
  - CoNLL-X
  language_id: 421026389
```

## __Cool__

```yml
%YAML 1.2
---
Cool:
  type: programming
  extensions:
  - ".cl"
  tm_scope: source.cool
  ace_mode: text
  language_id: 68
```

## __Coq__

```yml
%YAML 1.2
---
Coq:
  type: programming
  color: "#d0b68c"
  extensions:
  - ".coq"
  - ".v"
  tm_scope: source.coq
  ace_mode: text
  language_id: 69
```

## __Cpp-ObjDump__

```yml
%YAML 1.2
---
Cpp-ObjDump:
  type: data
  extensions:
  - ".cppobjdump"
  - ".c++-objdump"
  - ".c++objdump"
  - ".cpp-objdump"
  - ".cxx-objdump"
  tm_scope: objdump.x86asm
  aliases:
  - c++-objdump
  ace_mode: assembly_x86
  language_id: 70
```

## __Creole__

```yml
%YAML 1.2
---
Creole:
  type: prose
  wrap: true
  extensions:
  - ".creole"
  tm_scope: text.html.creole
  ace_mode: text
  language_id: 71
```

## __Crystal__

```yml
%YAML 1.2
---
Crystal:
  type: programming
  color: "#000100"
  extensions:
  - ".cr"
  ace_mode: ruby
  codemirror_mode: crystal
  codemirror_mime_type: text/x-crystal
  tm_scope: source.crystal
  interpreters:
  - crystal
  language_id: 72
```

## __CSON__

```yml
%YAML 1.2
---
CSON:
  type: data
  color: "#244776"
  tm_scope: source.coffee
  ace_mode: coffee
  codemirror_mode: coffeescript
  codemirror_mime_type: text/x-coffeescript
  extensions:
  - ".cson"
  language_id: 424
```

## __Csound__

```yml
%YAML 1.2
---
Csound:
  type: programming
  color: "#1a1a1a"
  aliases:
  - csound-orc
  extensions:
  - ".orc"
  - ".udo"
  tm_scope: source.csound
  ace_mode: csound_orchestra
  language_id: 73
```

## __Csound Document__

```yml
%YAML 1.2
---
Csound Document:
  type: programming
  color: "#1a1a1a"
  aliases:
  - csound-csd
  extensions:
  - ".csd"
  tm_scope: source.csound-document
  ace_mode: csound_document
  language_id: 74
```

## __Csound Score__

```yml
%YAML 1.2
---
Csound Score:
  type: programming
  color: "#1a1a1a"
  aliases:
  - csound-sco
  extensions:
  - ".sco"
  tm_scope: source.csound-score
  ace_mode: csound_score
  language_id: 75
```

## __CSS__

```yml
%YAML 1.2
---
CSS:
  type: markup
  tm_scope: source.css
  ace_mode: css
  codemirror_mode: css
  codemirror_mime_type: text/css
  color: "#563d7c"
  extensions:
  - ".css"
  language_id: 50
```

## __CSV__

```yml
%YAML 1.2
---
CSV:
  type: data
  color: "#237346"
  ace_mode: text
  tm_scope: none
  extensions:
  - ".csv"
  language_id: 51
```

## __Cuda__

```yml
%YAML 1.2
---
Cuda:
  type: programming
  extensions:
  - ".cu"
  - ".cuh"
  tm_scope: source.cuda-c++
  ace_mode: c_cpp
  codemirror_mode: clike
  codemirror_mime_type: text/x-c++src
  color: "#3A4E3A"
  language_id: 77
```

## __CUE__

```yml
%YAML 1.2
---
CUE:
  type: programming
  extensions:
  - ".cue"
  tm_scope: source.cue
  ace_mode: text
  color: "#5886E1"
  language_id: 356063509
```

## __Cue Sheet__

```yml
%YAML 1.2
---
Cue Sheet:
  type: data
  extensions:
  - ".cue"
  tm_scope: source.cuesheet
  ace_mode: text
  language_id: 942714150
```

## __cURL Config__

```yml
%YAML 1.2
---
cURL Config:
  type: data
  group: INI
  aliases:
  - curlrc
  filenames:
  - ".curlrc"
  - _curlrc
  tm_scope: source.curlrc
  ace_mode: text
  language_id: 992375436
```

## __CWeb__

```yml
%YAML 1.2
---
CWeb:
  type: programming
  color: "#00007a"
  extensions:
  - ".w"
  tm_scope: none
  ace_mode: text
  language_id: 657332628
```

## __Cycript__

```yml
%YAML 1.2
---
Cycript:
  type: programming
  extensions:
  - ".cy"
  tm_scope: source.js
  ace_mode: javascript
  codemirror_mode: javascript
  codemirror_mime_type: text/javascript
  language_id: 78
```

## __Cython__

```yml
%YAML 1.2
---
Cython:
  type: programming
  color: "#fedf5b"
  extensions:
  - ".pyx"
  - ".pxd"
  - ".pxi"
  aliases:
  - pyrex
  tm_scope: source.cython
  ace_mode: text
  codemirror_mode: python
  codemirror_mime_type: text/x-cython
  language_id: 79
```
