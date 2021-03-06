Installation
============

We assume you're familiar with `Composer <http://packagist.org>`_, a dependency manager for PHP.
Use the following command to add the bundle to your ``composer.json`` and download the package.

If you have `Composer installed globally <http://getcomposer.org/doc/00-intro.md#globally>`_.

.. code-block:: bash

    $ composer require sylius/promotion-bundle

Otherwise you have to download .phar file.

.. code-block:: bash

    $ curl -sS https://getcomposer.org/installer | php
    $ php composer.phar require sylius/promotion-bundle

Adding required bundles to the kernel
-------------------------------------

You need to enable the bundle inside the kernel.

If you're not using any other Sylius bundles, you will also need to add ``SyliusResourceBundle`` and its dependencies to kernel.
Don't worry, everything was automatically installed via Composer.

.. code-block:: php

    <?php

    // app/AppKernel.php

    public function registerBundles()
    {
        $bundles = array(
            new FOS\RestBundle\FOSRestBundle(),
            new JMS\SerializerBundle\JMSSerializerBundle($this),
            new Stof\DoctrineExtensionsBundle\StofDoctrineExtensionsBundle(),
            new WhiteOctober\PagerfantaBundle\WhiteOctoberPagerfantaBundle(),
            new winzou\Bundle\StateMachineBundle\winzouStateMachineBundle(),
            new Sylius\Bundle\ResourceBundle\SyliusResourceBundle(),
            new Sylius\Bundle\PromotionBundle\SyliusPromotionBundle(),

            // Other bundles...
            new Doctrine\Bundle\DoctrineBundle\DoctrineBundle(),
        );
    }


Promotion Subject configuration
-------------------------------

.. note::

    You need to have a class that is :doc:`registered as a sylius_resource </components_and_bundles/bundles/SyliusResourceBundle/configuration>`.
    It can be for example a ``CarRentalOrderClass``.

* Make your ``CarRentalOrder`` class implement the ``PromotionSubjectInterface``.

Put its configuration inside your ``app/config/config.yml``.

.. code-block:: yaml

    # app/config/config.yml
    sylius_promotion:
        resources:
            promotion_subject:
                classes:
                    model: AppBundle\Entity\CarRentalOrder

And configure doctrine extensions which are used by the bundle.

.. code-block:: yaml

    # app/config/config.yml
    stof_doctrine_extensions:
        orm:
            default:
                timestampable: true

Congratulations! The bundle is now installed and ready to use.
