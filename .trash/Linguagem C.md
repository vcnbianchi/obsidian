---
title: Linguagem C
author: Victor Bianchi
created at: 2026-10-20
updated at: 2026-10-21
---
# Sumário

1. [Introdução](#Introdução)
2. [ANSI C](#ANSI%20C)
# Introdução

A linguagem C foi criada em **1972** por **Dennis M. Ritchie** nos laboratórios da **Bell Labs**. Em **1978**, **Brian W. Kernighan** e o próprio **Ritchie** publicaram a primeira edição do livro **_The C Programming Language_** (conhecido como **K&R**), que se tornou a **referência informal da linguagem**. A segunda edição, de **1988**, já descreve a versão padronizada que viria a ser conhecida como **ANSI C**, a **referência formal** da linguagem.

Nos anos seguintes à publicação do K&R, C deixou de ser apenas a linguagem do sistema operacional UNIX e se espalhou por muitos outros ambientes. Com o crescimento da popularidade, surgiram dezenas de compiladores feitos por grupos que não tinham participado do projeto original. Cada um desses compiladores interpretava algumas partes da linguagem de forma ligeiramente diferente. O mesmo programa podia se comportar de um jeito em uma máquina e de outro jeito em outra. Um exemplo disso são extensões proprietárias, como a função `_C_Get_Ssn_Handle`, presente apenas nos compiladores _ILE C/C++_ da IBM e inexistente em qualquer outro ambiente.

Essas divergências, somadas às mudanças naturais que a linguagem sofreu ao longo dos anos, tornaram clara a necessidade de uma definição oficial, precisa e portável. Em 1983, a **_American National Standards Institute_** **(ANSI)** formou um comitê com o objetivo explícito de produzir o que eles chamaram de: “_an unambiguous and machine-independent definition of the language C_”, isto é, **uma definição da linguagem C que fosse não ambígua e independente de máquina**, sem, contudo, perder o espírito original da linguagem. O resultado desse trabalho foi o padrão **ANSI C**, publicado em **1989**.
# ANSI C

Anteriormente à criação do ANSI C, a única referência existente da linguagem era a primeira edição do K&R. Quando a ANSI criou o comitê, o objetivo era justamente produzir uma referência formal escrita de forma jurídica e técnica, que servisse de contrato entre:

- Quem escreve programas;
- Quem escreve compiladores.

Esse documento oficial é o padrão **ANSI C (ANSI X3.159-1989)**, depois adotado internacionalmente como **ISO/IEC 9899:1990** (conhecido como **C90**).