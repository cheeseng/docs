Setup and use Play framework 2.0 in Scala IDE 2.0
=================================================

|frflag| :doc:`version française<index-fr>`

.. |frflag| image:: ../../user/images/frflag.png

What is in this guide?
----------------------

This guide will show you how to configure a Play web application to import it in Scala IDE, how to configure `Scala IDE`_ to work fine with the Play framework and finally how to develop Play web application from inside Scala IDE.

Prerequisites
.............

*   `Eclipse`_ 3.6.2 (Helios) with Scala IDE for Scala 2.9 installed (update site: http://download.scala-ide.org/releases-29/stable/site).

    Check the :ref:`getting started <gettingstarted_getting-started>` page for instructions on how to install Scala IDE.

*   A basic knowledge of the Eclipse user interface is required.

*   No knowledge of the Scala language is required (in this guide).

*   No knowledge of the Play framework is required (in this guide).

Setting up Play 2.0
-------------------

To be able to create a Play web application, the Play framework need to be installed. If you have not installed it already, follow this few steps, or use the `Play documentation`_.

*   Download Play framework 2.0-beta from http://www.playframework.org/2.0.

*   Unzip it in your preferred location. Let's say ``/path/to/play20`` for the purpose of this document.

*   For convenience, add the Play folder to your system PATH:

    .. code-block:: bash

       export PATH=$PATH:/path/to/play20

Creating a Play 2.0 application
-------------------------------

*   In your development folder, ask Play to create a new web application, as a ``simple Scala application``.

    .. image:: images/play20-scalaide20-01.png
       :alt: play new testApp
       :width: 100%
       :target: ../../_images/play20-scalaide20-01.png

*   Go into the application folder.

    .. image:: images/play20-scalaide20-02.png
       :alt: cd testApp
       :width: 100%
       :target: ../../_images/play20-scalaide20-02.png

*   And launch Play.

    .. image:: images/play20-scalaide20-03.png
       :alt: play
       :width: 100%
       :target: ../../_images/play20-scalaide20-03.png

*   In Play, launch your newly created web application.

    .. image:: images/play20-scalaide20-04.png
       :alt: run
       :width: 100%
       :target: ../../_images/play20-scalaide20-04.png

*   Check that the application works: http://localhost:9000/.

    .. image:: images/play20-scalaide20-05.png
       :alt: running
       :width: 100%
       :target: ../../_images/play20-scalaide20-05.png

Configuring the Play 2.0 web application for Scala IDE
------------------------------------------------------

Now that the Play application is running, it needs to be configured so it can be imported into Scala IDE.

The eclipsify support is not yet integrated it Play 2.0, so we are using `sbteclipse`_ to make it an Eclipse project.

*   First, exit Play using ``ctrl-d``, and then ``exit``.

    .. image:: images/play20-scalaide20-06.png
       :alt: ctrl-d, exit
       :width: 100%
       :target: ../../_images/play20-scalaide20-06.png

*   Add sbteclipse to sbt by creating the ``project/build.sbt`` file and adding the following lines.

    .. code-block:: scala

       
       resolvers += Classpaths.typesafeResolver
       
       addSbtPlugin("com.typesafe.sbteclipse" % "sbteclipse" % "1.5.0")

    .. image:: images/play20-scalaide20-07.png
       :alt: modify project/build.sbt
       :width: 100%
       :target: ../../_images/play20-scalaide20-07.png

*   Go back into Play.

    .. image:: images/play20-scalaide20-08.png
       :alt: play
       :width: 100%
       :target: ../../_images/play20-scalaide20-08.png

*   Generate the Eclipse project configuration.

    .. image:: images/play20-scalaide20-09.png
       :alt: eclipse
       :width: 100%
       :target: ../../_images/play20-scalaide20-09.png

*   And relaunch the web application, so it is available later.

    .. image:: images/play20-scalaide20-10.png
       :alt: run
       :width: 100%
       :target: ../../_images/play20-scalaide20-10.png

Configuring Scala IDE for the Play 2.0 web application
------------------------------------------------------

Setting a few preferences in Eclipse will make everything easier to use.

*   Open the internal web browser view in Eclipse, and check you can access your web application.

    .. image:: images/play20-scalaide20-12.png
       :alt: http://localhost:9000/
       :width: 100%
       :target: ../../_images/play20-scalaide20-12.png

*   Configure Eclipse so changes on the filesystem are automatically picked up.

    .. image:: images/play20-scalaide20-13.png
       :alt: refresh automatically
       :width: 100%
       :target: ../../_images/play20-scalaide20-13.png

*   If you don't have the Web Development Tools for Eclipse installed, Eclipse opens ``.html`` files in a web browser. Configure it to use the ``Scala Editor`` instead.

    .. image:: images/play20-scalaide20-14.png
       :alt: HTML file in text editor
       :width: 100%
       :target: ../../_images/play20-scalaide20-14.png

Importing the Play web application into Scala IDE
-------------------------------------------------

Everything is setup, it is time to import the project in the IDE.

*   Import the Play 2.0 application as an ``Existing Projects into Workspace``.

    .. image:: images/play20-scalaide20-15.png
       :alt: import project
       :width: 100%
       :target: ../../_images/play20-scalaide20-15.png

*   Everything is good, everything compiles.

    .. image:: images/play20-scalaide20-16.png
       :alt: everything compiles
       :width: 100%
       :target: ../../_images/play20-scalaide20-16.png

Doing some development
----------------------

Now that everything is setup, we can change the content. Let's add a way to have a quote on the main page.

*   First, create the ``models.Quote`` class using the new ``Scala Class`` wizard.

    .. image:: images/play20-scalaide20-19.png
       :alt: create model.Quote
       :width: 100%
       :target: ../../_images/play20-scalaide20-19.png

*   Add variables to ``models.Quote``.

    .. code-block:: scala

       package models
       
       case class Quote(val text: String, val author: String) {
       
       }

*   Add an extra parameter to the ``index.scala.html`` view and update the layout.

    .. code-block:: scala

       @(message: String, quote: models.Quote)
       
       @main("Welcome to Play 2.0 beta") {
       
           @play20.welcome(message)
           
           <p>@quote.text<em> - @quote.author</em></p>
       
       }

*   The templates are transformed into Scala code by the Play framework, so use the ``refresh`` button in the internal web browser to trigger it.

    Play returns a compilation error, the application is not using the template correctly. The error is also visible in the code of ``Application.scala``.
    
    .. image:: images/play20-scalaide20-17.png
       :alt: compilation error
       :width: 100%
       :target: ../../_images/play20-scalaide20-17.png

*   Fix the application code, using a smart quote.

    .. code-block:: scala

         def index = Action {
           Ok(views.html.index("Your new application is ready.",
               Quote("Citer les pensees des autres, c'est regretter de ne pas les avoir trouvees soi-meme.",
                   "Sacha Guitry")))
         }

*   The code compiles. Check the result in the internal web browser.

    .. image:: images/play20-scalaide20-18.png
       :alt: done
       :width: 100%
       :target: ../../_images/play20-scalaide20-18.png

Going further
-------------

You now have all you need to create great web applications with Play 2.0 and Scala.

For more information about Play 2.0, check out the `Play 2.0 wiki`_.

For more information about Scala, go to the `documentation website`_ or get the downloadable `eBook`_.


.. _Scala IDE: http://www.scala-ide.org
.. _Eclipse: http://www.eclipse.org/
.. _Play documentation: https://github.com/playframework/Play20/wiki/Installing
.. _sbteclipse: https://github.com/typesafehub/sbteclipse
.. _Play 2.0 wiki: https://github.com/playframework/play20/wiki
.. _documentation website: http://docs.scala-lang.org/
.. _eBook: http://typesafe.com/resources/scala-for-the-impatient