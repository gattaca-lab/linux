===================================
  TBI support for RISCV
===================================

Alexey Baturo <baturo.alexey@gmail.com>, Apr 2020
Anatoly Parshintsev <kupokupokupopo@gmail.com>, Apr 2020

Introduction
------------

In order to support TBI a new register TBICONTROL (0x800) was intoduced.

At the present moment non-priviledged SW can access (and change it).
If TBICONTROL[0] is "1" then  TBI is enabled for the current thread of execution.

Linux context switching routines were adjusted in a such a way that
every scheduled thread can have it's own value.
