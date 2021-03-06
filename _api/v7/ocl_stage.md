---
version: 7
name: ocl.Stage
title: ocl.Stage
description: |
  The definition of a Stage.
type: class
code_block:
  title: Example Stage
  language: m
  code: |-
    stage = ocl.Stage([], @vars, @ode, 'N', 10, 'd', 2);

    % Function definitions can be in the same file
    % (if the main script is wrapped by a function)
    % or in separate files:
    function vars(sh)
      sh.addState('s');
      sh.addState('v');
    end

    function ode(sh,x,~,~,~)
      sh.setODE('s', x.v);
      sh.setODE('v', -10);
    end

parameters:

  - name: "T"
    content: "The end time/horizon length of the optimal control problem. If your system equations are expressed as function of an independent variable other than time, `T` represents not the end time but the endpoint of the integration over the independent variable. If you would like to optimize for time, **time optimal control**, pass the empty list `[]`."
    type: "numeric or []"

  - name: vars
    content: "System variables function. Defaults to an empty function handle."
    type: "[@(vh)](#api@vars)"

  - name: dae
    content: "DAE (system equations) function. Defaults to an empty function handle."
    type: "[@(daeh,x,z,u,p)](#api@dae)"

  - name: pathcosts
    content: "Path-cost function. Defaults to a function handle returning `0`."
    type: "[@(costh,x,z,u,p)](#api@pathcost)"

  - name: gridcosts
    content: "Grid-cost function. Defaults to a function handle returning `0`."
    type: "[@(costh,k,K,x,p)](#api@gridcost)"

  - name: gridconstraints
    content: "Grid-constraints function. Defaults to no constraints added."
    type: "[@(conh,k,K,x,p)](#api@gridcost)"

  - name: terminalcost
    content: "Terminal cost function. Defaults to a function handle returning `0`."
    type: "[@(ch,x,p)](#api@terminalcost)"

  - name: N
    content: "Number of control intervals. Defaults to `20`."
    type: Integer

  - name: d
    content: "Degree of the interpolating polynomial in each control interval. Defaults to `3`."
    type: Integer in [2,5]

  - name: userdata
    content: "A data field that can be used to pass any kind of constant data to the model functions. The userdata can be accessed by using the `userdata` property of `ocl.Cost`, `ocl.Constraint`, `ocl.DaeHandler`, and `ocl.VarHandler`. Defaults to an empty list."
    type: Any type, for example a struct or list.

methods:
  - name: "setBounds"
    content: "Sets a bound on a variable for the whole trajectory. If only the lower bound is given, it will be `lb==ub`."
    parameters:
      - content: "The variable id"
        name: "id"
        type: "string"
      - content: "The lower bound"
        name: "lb"
        type: "numeric"
      - content: "The upper bound"
        name: "ub"
        type: "numeric,optional"
  - name: "setInitialBounds"
    content: "Sets an initial bound on a variable. If only the lower bound is given, it will be `lb==ub`."
    parameters:
      - content: "The variable id"
        name: "id"
        type: "string"
      - content: "The lower bound"
        name: "lb"
        type: "numeric"
      - content: "The upper bound"
        name: "ub"
        type: "numeric,optional"
  - name: "setEndBounds"
    content: "Sets an end bound on a variable. If only the lower bound is given, it will be `lb==ub`."
    parameters:
      - content: "The variable id"
        name: "id"
        type: "string"
      - content: "The lower bound"
        name: "lb"
        type: "numeric"
      - content: "The upper bound"
        name: "ub"
        type: "numeric,optional"
  - name: "initialize"
    content: "Sets an initial guess for a variable."
    parameters:
      - content: "The variable id"
        name: "id"
        type: "string"
      - content: "The normalized gridpoints. The gridpoints is a list of values between `0` and `1` where `0` is the beginning of the trajectory and `1` is the final time of the trajectory."
        name: "gridpoints"
        type: "numeric"
      - content: "The initial guess values at the gridpoints. The number of columns of `values` must be equal to the length of `gridpoints`."
        name: "values"
        type: "numeric"

position: 10
returns: ~
---
