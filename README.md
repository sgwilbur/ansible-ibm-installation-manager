### IBM Installation Manager

Install the IBM Installation Manager that provides that base installation mechanism for a number of IBM products.

Download the lastest installer from ibm.com, you can start at the [IBM Installation Manager and Package Utility landing page](http://www-01.ibm.com/support/docview.wss?uid=swg27025142) and follow the links to the version you are looking for.

#### About

This is a basic cross platform installer technology, for an IBM package management solution that applies to many Rational products, some UrbanCode, some Tivoli, some WebSphere, and probably others. This playbook is just meant to perform the basic default install to `/opt/IBM/InstallationManager` with most of the logic hard-coded for simplicity.

To use select the matching version of this playbook to the version of Installation Manager you wish to use, that way I will have hard-coded the variables you need into the playbook. Otherwise you can pass the additional variables into the role to override these, say if I have not yet created a version for an newer/older IM client.

#### Using the playbook

Install from galaxy

    ansible-galaxy install sgwilbur.ibm-installation-manager

Include the role in your plybook:

    vars:
    - staging_media_host: http://192.168.1.65:8000

    roles:
    - { role: sgwilbur.ibm-installation-manager, media_host: "{{ staging_media_host }}" }

Or the more advanced version( see `defaults\main.yml` for variables ) say to install a different version or architecture, currently the playbook only supports Ubuntu linux so you won't be able to easily change that variable:

    roles:
    - { role: sgwilbur.ibm-installation-manager, media_host: "{{ staging_media_host }}", arch: "x86", version: "1.8.4.0", version_tag: "1.8.4000.20151125_0201" }

#### Staging your media

 The playbook expects that you stage your media to a HTTP server and provide the base path, see `tasks/main.yml` for the `Download local copy of installer` task where we construct this url.

    url={{ media_host }}/software/ibm/installation_manager/{{ version }}/agent.installer.{{ platform }}.gtk.{{ architecture }}_{{ version_tag }}.zip

So this requires that you the media hosted at `/software/ibm/installation_manager/{version}/` and the rest is keyed off of your version and architecture.

#### Supported Platforms

My primary work is on Ubuntu and for the past year or so I have only been playing around with Trusty, so YMMV for earlier versions.

#### Contributing

I am just getting started with creating my first few playbooks, so I am learning as I go. If you have the know how and desire, I welcome contributions to improve the playbook, add platforms, or any other meaningful contributions or just constructive suggestions if you see something blatantly missing. So please fork, send me pull requests, and/or open issues.
