---
title: "ML07 - Recurrent Neural Networks"
---

일련의 벡터 $x$에 대하여 각 시점마다 아래의 재귀 공식을 적용하여 처리할 수 있습니다.

<div>$$
{ h }_{ t } = { f }_{ W }({ h }_{ t-1 },{ x }_{ t })
$$</div>

## Vanilla Recurrent Neural Network

상태가 하나의 hidden 벡터 $h$로 이루어지는 경우 vanilla RNN이라고 말합니다.

<div>$$
h_t=tanh(W_{hh}h_{t-1}+W_{xh}x_t) \\
y_t=W_{hy}h_t
$$</div>

## 참고 문서

1. [Recurrent Neural Networks](http://cs231n.stanford.edu/slides/2017/cs231n_2017_lecture10.pdf) from CS231n - Spring 2017