---
title: 'ESPHome Docs'
discription: 'One of the areas of ESPHome that can always be improved is the documentation.
If you see an issue somewhere, a spelling mistakes or if you want to share your awesome
setup, please feel free to submit a pull request.'
menu:
  main:
    parent: contrib
    weight: 4
---

## Contributing to ESPHome-Docs
The ESPHome documentation is built using `sphinx <http://www.sphinx-doc.org/>`** and uses
`reStructuredText <http://docutils.sourceforge.net/rst.html>`** for all source files.

If you're not familiar with writing rST, see :ref:`rst-syntax` for a quick refresher.


Build

* * *

.. note::

    The easiest way is to use the `esphome-docs container image <ghcr.io/esphome/esphome-docs/>`__:

    .. code-block:: bash

        docker run --rm -v "${PWD}/":/data/esphomedocs -p 8000:8000 -it ghcr.io/esphome/esphome-docs

    With ``PWD`` referring to the root of the ``esphome-docs`` git repository. Then go to ``<CONTAINER_IP>:8000`` in your browser.

    This way, you don't have to install the dependencies to build the documentation.

To check your documentation changes locally, you first need install Sphinx (with **Python 3**).

.. code-block:: bash

    # in ESPHome-Docs repo:
    pip install -r requirements.txt

Then, use the provided Makefile to build the changes and start a live-updating web server:

.. code-block:: bash

    # Start web server on port 8000
    make live-html

Notes

* * *

Some notes about the docs:

-   Use the English language (duh...)
-   An image tells a thousand words, please use them wherever possible. But also don't forget to shrink them, for example
    I often use <https://tinypng.com/>
-   Try to use examples as often as possible (also while it's great to use highly accurate,
    and domain-specific lingo, it should not interfere with new users understanding the content)
-   Fixes/improvements for the docs themselves should go to the `current` branch of the
    esphomedocs repository. New features should be added against the `next` branch.
-   Always create new branches in your fork for each pull request.

.. \_rst-syntax:

Syntax

* * *

Here's a quick RST primer:

Title hierarchy is based on order of occurrence, not on type of character used to underline it. This
documents establish the following character order for better consistency.

-   **Headers**: You can write titles like this:

    .. code-block:: rst

        My Title
        ========

    and section headers like this:

    .. code-block:: rst

        My Sub Section
        --------------

    and sub-section headers like this:

    .. code-block:: rst

        My Sub-sub Section
        ******************

    .. note::

        The length of the bar below the text **must** match the title Text length.
        Also, titles should be in Title Case

-   **Links**: To create a link to an external resource (for example <https://www.google.com>), use
    ``\`Link text <link_url>\`__``. For example:

    .. code-block:: rst

        `Google.com <https://www.google.com>`__

    `Google.com <https://www.google.com>`\_\_

-   **References**: To reference another document, use the `:doc:` and `:ref:` roles (references
    are set up globally and can be used between documents):

    .. code-block:: rst

        .. _my-reference-label:

        Section to cross-reference
        --------------------------

        See :ref:`my-reference-label`, also see :doc:`/components/switch/gpio`.
        :doc:`Using custom text </components/switch/gpio>`.

    See :ref:`devices`, also see :doc:`/components/switch/gpio`.
    :doc:`Using custom text </components/switch/gpio>`.

-   **Inline code**: To have text appear `like this`, use double backticks:

    .. code-block:: rst

        To have text appear ``like this``, use double backticks.

    To have text appear `like this`, use double backticks.

-   **Code blocks**: To show a sample configuration file, use the `code-block` directive:

    .. code-block:: rst

        .. code-block:: yaml

            # Sample configuration entry
            switch:
              - platform: gpio
                name: "Relay #42"
                pin: GPIO13

    .. code-block:: yaml

        # Sample configuration entry
        switch:
          - platform: gpio
            name: "Relay #42"
            pin: GPIO13

    .. note::

        Please note the empty line after the ``code-block`` directive. That is necessary.

-   **Images**: To show images, use the `figure` directive:

    .. code-block:: rst

        .. figure:: images/dashboard_states.png
            :align: center
            :width: 40.0%

            Optional figure caption.

    .. figure:: images/dashboard_states.png
        :align: center
        :width: 40.0%

        Optional figure caption.

    .. note::

        All images in the documentation need to be as small as possible to ensure
        fast page load times. For normal figures the maximum size should be at most
        about 1000x800 px or so. Additionally, please use online tools like
        https://tinypng.com/ or https://tinyjpg.com/ to further compress images.

-   **Notes and warnings**: You can create simple notes and warnings using the `note` and `warning`
    directives:

    .. code-block:: rst

        .. note::

            This is a note.

        .. warning::

            This is a warning.

    .. note::

        This is a note.

    .. warning::

        This is a warning.

-   **Italic and boldface font families**: To _italicize_ text, use one asterisk around the text. To put
    **a strong emphasis** on a piece of text, put two asterisks around it.

    .. code-block:: rst

        *This is italicized.* (A weird word...)
        **This is very important.**

    _This is italicized._ (A weird word...)
    **This is very important.**

-   **Ordered and unordered list**: The syntax for lists in RST is more or less the same as in Markdown:

    .. code-block:: rst

        - Unordered item

          - Unordered sub-item

        - Item with a very long text so that it does not fully fit in a single line and
          must be split up into multiple lines.

        1. Ordered item #1
        2. Ordered item #2

    -   Unordered item

        -   Unordered sub-item

    -   Item with a very long text so that it does not fully fit in a single line and
        must be split up into multiple lines.

    1.  Ordered item #1
    2.  Ordered item #2

-   **imgtable**: ESPHome uses a custom RST directive to show the table on the front page (see
    `index.rst <https://github.com/esphome/esphome-docs/blob/current/index.rst>`\_\_).
    New pages need to be added to the `imgtable` list. The syntax is CSV with <PAGE NAME>, <FILE NAME> (without RST),
    <IMAGE> (in top-level images/ directory), <COMMENT> (optional - short text to describe the component). The aspect ratio of these images should be 8:10 (or 10:8) but exceptions are possible.

    Because these images are served on the main page, they need to be compressed heavily. SVGs are preferred over JPGs
    and JPGs should be max. 300x300px.
    If you have imagemagick installed, you can use this command to convert the thumbnail:

    .. code-block:: bash

        convert -sampling-factor 4:2:0 -strip -interlace Plane -quality 80% -resize 300x300 in.jpg out.jpg

reStructured text can do a lot more than this, so if you're looking for a more complete guide
please have a look at the `Sphinx reStructuredText Primer <http://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html>`\_\_.
