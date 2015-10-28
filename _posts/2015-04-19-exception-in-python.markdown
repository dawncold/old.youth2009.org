---
layout: post
title: "exception in python"
date: 2015-04-19 17:05:31 +0800
comments: true
categories: dev
---

My colleague remembered that if you pass some `kwargs` to an `Exception` subclass e.g. `class MyException(Exception): pass`, you will get a composed message when you catch the exception and call `e.message`. Unitil we got nothing from one place which it should display exception's message, python language part is implemented by C, so we downloaded python source code(2.7.9), and find these lines.

```c
static int
BaseException_init(PyBaseExceptionObject *self, PyObject *args, PyObject *kwds)
{
    if (!_PyArg_NoKeywords(Py_TYPE(self)->tp_name, kwds))
        return -1;

    Py_DECREF(self->args);
    self->args = args;
    Py_INCREF(self->args);

    if (PyTuple_GET_SIZE(self->args) == 1) {
        Py_CLEAR(self->message);
        self->message = PyTuple_GET_ITEM(self->args, 0);
        Py_INCREF(self->message);
    }
    return 0;
}
```
This is python BaseException's C implementation, I can understand logic but C syntax. The BaseException accepts `kwargs`, but if you pass a `kwargs` to Exception, you will get a warning, because of `_PyArg_NoKeywords`, maybe it needs compatibility with old code, but now, you can't use `kwargs`.

Another notice, if you pass one argument to it, this argument will be the `e.message` value, if not, your args will be placed in `e.args`.

We finally implemented `__str__` and `__unicode__` methods, because of we imported `unicode_literals`, so we think this is the best practice, we just use `str(e)` in those places.

```python

class TmallAPIException(Exception):
    def __init__(self, code, msg, sub_code, sub_msg):
        super(TmallAPIException, self).__init__(code, msg, sub_code, sub_msg)
        self.code = code
        self.msg = msg
        self.sub_code = sub_code
        self.sub_msg = sub_msg

    def __unicode__(self):  # TODO: not necessary under python3
        return 'code: {}, msg: {}, sub_code: {}, sub_msg: {}'.format(self.code, self.msg, self.sub_code, self.sub_msg)

    def __str__(self):
        return self.__unicode__().encode('utf-8')
```