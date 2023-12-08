---
title: 'ESPHome Docs'
menu:
  main:
    parent: contrib
    weight: 4
---

## Contributing to ESPHome-Docs

.. image:: /images/logo-docs.svg
    :align: center
    :width: 60.0%
    :class: dark-invert

One of the areas of ESPHome that can always be improved is the documentation.
If you see an issue somewhere, a spelling mistakes or if you want to share your awesome
setup, please feel free to submit a pull request.

The ESPHome documentation is built using `sphinx <http://www.sphinx-doc.org/>`** and uses
`reStructuredText <http://docutils.sourceforge.net/rst.html>`** for all source files.

If you're not familiar with writing rST, see :ref:`rst-syntax` for a quick refresher.

Through Github

* * *

This guide essentially goes over the same material found in `GitHub's Editing files in another user's repository <https://docs.github.com/en/repositories/working-with-files/managing-files/editing-files#editing-files-in-another-users-repository>`\_\_. You may also find that page helpful to read.

At the bottom of each page in the docs, there is a "Edit this page on GitHub" link. Click this link and you'll see something like this:

.. figure:: images/docs_ghedit_1.png
    :align: center
    :width: 80.0%
    :alt: a screenshot of an rST file opened in GitHub, with the edit button circled

Click the edit button to start making changes. If you're not sure about some element of syntax, see the quick-start :ref:`rst-syntax` guide.

Once you've made your changes, give them a useful name and press "Propose changes". At this point, you've made the changes on your own personal copy of the docs in GitHub, but you still need to submit them to us.

.. figure:: images/docs_ghedit_2.png
    :align: center
    :width: 80.0%
    :alt: the commit creation screen in GitHub, with the commit title and "Propose changes" button circled

To do that, you need to create a "Pull request":

.. figure:: images/docs_ghedit_3.png
    :align: center
    :width: 80.0%
    :alt: the pull request prompt screen in GitHub with the "Create pull request" button circled

Fill out the new pull request form, replacing the `[ ]` with `[x]` to indicate that you have followed the instructions.

.. figure:: images/docs_ghedit_4.png
    :align: center
    :width: 80.0%
    :alt: the pull request creation screen in GitHub with the "Create pull request" button circled

After waiting a while, you might see a green or a red mark next to your commit in your pull request:

.. figure:: images/docs_ghedit_ci_failed.png
    :align: center
    :width: 80.0%
    :alt: the pull request with a commit with a red x next to it

This means that there is some error stopping your pull request from being fully processed. Click on the X, click on "Details" next to the lint step, and look and see what's causing your change to fail.

.. figure:: images/docs_ghedit_ci_details.png
    :align: center
    :width: 80.0%
    :alt: failed lint substep of build, with "details" link circled

.. figure:: images/docs_ghedit_ci_logs.png
    :align: center
    :width: 80.0%
    :alt: log messages showing reason for failed build

For example, in this case, you'd want to go to line 136 of `pzemac.rst` and adjust the number of `===` so that it completely underlines the section heading.

Once you make that change, the pull request will be built again, and hopefully this time where will be no other errors.

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
