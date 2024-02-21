---
layout: post
date: 2024/02/21 07:03 +0100
title: Looks like a protected attribute but it's not
category: python
---
I needed a way to know if an instance of a django model is new, and I asked [gemini](https://gemini.google.com). It said I should use `instance._state.adding`. With my small python knowledge, I know `_state` is supposed to be a protected attribute and I should not depend on it, especially outside the instance.

I then set course and hoisted my sails in pursuit of answers.

I immediately reached a [stackoverflow question](https://stackoverflow.com/questions/907695/in-a-django-model-custom-save-method-how-should-you-identify-a-new-object), and I then dropped my anchor. One [answer](https://stackoverflow.com/a/907703) said:

> Updated: With the clarification that self._state is not a private instance variable, but named that way to avoid conflicts, checking self._state.adding is now the preferable way to check.

I couldn't find where he / she got the clarification, perhaps he / she is an authority in the django-*island*.

Diving deeper and looking closely into the [documentation](https://docs.djangoproject.com/en/5.0/ref/models/instances/), I saw:

> The _state attribute refers to a ModelState object that tracks the lifecycle of the model instance.

Well, they said it's an attribute, nothing about protected-ness, and the docs is an API reference. If they wouldn't want me to use it, they would have said something about it there.

## Conclusion

With this, I have the green light to use `instance._state` in my django code.
