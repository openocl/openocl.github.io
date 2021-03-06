---
version: 5
name: ocl.System
title: "ocl.System"
type: class
description: |-
  A dynamical system is defined by implementing functions for the system variables and equations, and creating an OclSystem passing the function pointers. You need to implement two functions, one for defining the system variables, and a second one for defining the system equations. The system is created by passing the handles of the two functions to the constructor of OclSystem. A system can be used width an [ocl.Simulator](#apiocl_simulator).

code_block:
  title: Example System
  language: m
  code: |-
    sys = OclSystem(@sysVars,@sysEq);

    % Function definitions can be in the same file
    % (if the main script is wrapped by a function)
    % or in separate files:
    function sysVars(svh)
      svh.addState('p');
      svh.addState('v');
      svh.addControl('u');  
    end
    function sysEq(seh,x,z,u,p)
      seh.setODE('p',(1-x.v^2)*x.p-x.v+u.u);
      seh.setODE('v',x.p);
    end
parameters:
  - name: "vars"
    default: "@(vars_handler)[]"
    content: "System variables function. Optional, defaults to an empty function handle."
    type: "[@(vars_handler)](#apiocl_@(vars_handler))"

  - name: dae
    default: "@(dae_handler,x,z,u,p)[]"
    content: "DAE (system equations) function. Optional, defaults to an empty function handle."
    type: "[@(dae_handler,x,z,u,p)](#apiocl_@(dae_handler,x,z,u,p))"
returns: ~
---
