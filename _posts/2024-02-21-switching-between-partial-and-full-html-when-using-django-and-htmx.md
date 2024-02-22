---
layout: post
title: Switching between partial and full html when using django and htmx
categories: python django
date: 2024/02/22 19:04:00 +0100
---
I created a [context processor](https://docs.djangoproject.com/en/5.0/ref/templates/api/#context-processors) to help me switch between full and partial templates in [django](https://www.djangoproject.com) automatically. It sets my base template to a partial template if the request is a [`htmx`](https://htmx.org) request.

## TL;DR

I just check if the current request is a `htmx` request, then I set the base template to `_partial.html`, else `_base.html`.

## The code

### `myApp/context_processors.py`

```python
from django.http import HttpRequest


def setBaseTemplate(request: HttpRequest) -> dict[str, str]:
    """Sets the base_template context variable.
    Parameters:
    - request: Request object.
    Returns:
    - dict: A dictionary that sets either '_base.html' or '_partial.html' as the base template.
    """
    baseTemplate = '_partial.html' if request.htmx else '_base.html'
    return {'base_template': baseTemplate}
```

### `myProject/settings.py`

To activate the context processor, I added it to the list of context processors for my template engine [django template](https://docs.djangoproject.com/en/5.0/ref/templates/language/). I opened my `settings.py` file, moved down to where the list `TEMPLATES` is defined and added it to the `context_processors` list;

```python
TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",
        "DIRS": [],
        "APP_DIRS": True,
        "OPTIONS": {
            "context_processors": [
                "django.template.context_processors.debug",
                "django.template.context_processors.request",
                "django.contrib.auth.context_processors.auth",
                "django.contrib.messages.context_processors.messages",
                "myApp.context_processors.setBaseTemplate",
            ],
        },
    },
]
```

The new context processor is **`"myApp.context_processors.setBaseTemplate"`**.

## Explanation

I will be building my explanation on that of [django-htmx](https://django-htmx.readthedocs.io/en/latest) [tips](https://django-htmx.readthedocs.io/en/latest/tips.html).

If you have your templates setup as `django-htmx` suggested, then your templates will be expecting a `base_template` variable. That variable will determine which base template to use.

From [django docs](https://docs.python.org/3/library/stdtypes.html#dict):

> Context processors are functions that receive the current HttpRequest as an argument and return a dict of data to be added to the rendering context.

> Their main use is to add common data shared by all templates to the context without repeating code in every view.

Instead of having to pass the `base_template` variable each time I want to render a template, my context processor automatically sets it for me. I need only the main html chunk when it's a `htmx` request, so I set the base template to `_partial.html`. Otherwise, I set it to `_base.html`, which is a full html file.

## Conclusion

This will work until there is an exception to the assumption. In that case, I am planning to add an attribute to the `request` object to let my `context processor` know about the exception. Until then, this is perfect!

Perhaps django-htmx might like to add it to there extension, I'll open an issue and tell them about it.
