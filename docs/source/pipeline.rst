Whitelab Computational Resources
=================================

Officials to contact to receive access.
-----------------------------------------
To receive an account needed for accessing the whitelab servers within Rutgers, one needs to contact the
following persons for setting up an account,

Cheryl Thiemann cthiemann@cinj.rutgers.edu

Wenping Yang yangw3@cinj.rutgers.edu

Adrian Rodriguez alr252@cinj.rutgers.edu

Our Resources
------------------
We have 1 servers with the following configuration. This set up
is minimal to just hold


**Machine**
- RAM : 128 GB
- Disk Space : 3 TB (extendable)

Baic Usage
------------------
*How to get an account in whitelab servers?*
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Contact the officials mentioned above as you need several permissions to get an account.
After getting an account you need to use `VPN`_
to get connected with the whitelab server. The information for vpn is provided
in the Rutgers `IT website`_. Once connected to to VPN you can
use the following command to log in to the whitelab server.

*What do I need for logging in from a Mac?*

You can open the terminal app or use any other comamnd prompt to
log in to the whitelab server. The command is as follows,

.. code-block:: bash

        $ ssh <NetID>@wlab.cinj.rutgers.edu

You will be prompted to enter your passwird and after entering the password
you will be logged in to the whitelab server.

*What do do if I am using a Windows machine?*

As windows machines do not have a command prompt, you need to install
a software called `Mobaxterm <https://mobaxterm.mobatek.net/>`_ to
get a tool that can help you logging in the mobaxterm server. In the mobaxterm
app you can log in following the previous command

.. code-block:: bash

        $ ssh <NetID>@wlab.cinj.rutgers.edu


You will be prompted to enter your passwird and after entering the password
you will be logged in to the whitelab server.

*How to navigate through the server?*
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Whitelab server is a basic linux server that can be navigated using basic
linux commands. You can follow this `tutorial <https://ubuntu.com/tutorials/command-line-for-beginners#4-creating-folders-and-files>`_ to
learn about the basic linux commands to create directories and navigate
through the server. You can navigate the sytem by learning these commands from
`here <https://ubuntu.com/tutorials/command-line-for-beginners#5-moving-and-manipulating-files>`_ .
There are countless other resources including asking `chatgpt <https://chat.openai.com/>`_ to
learn about the basic linux commands.

*How the server is organized?*
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The server is organized in a way that you can find the data in the following,
individual users have their own home directory. Your home directory should be in
``/home/<NetID>``.

Consequently, all the data right now resides in ``/s3-data/white-lab-hirak/data``.
The data from the guest users are located in ``/s3-data/white-lab-hirak/users/guest-users``.
For example the data from the guest user `Hui` is located in
``/s3-data/white-lab-hirak/users/guest-users/Hui``.

*Maneuvering through the server*
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As mentioned you can follow this `tutorial <https://ubuntu.com/tutorials/command-line-for-beginners#4-creating-folders-and-files>`_ to
navigate the system. You would mostly use ``cd`` and ``ls`` to navigate through the system.
For example to see the contents of the ``/s3-data/white-lab-hirak/data`` you can use the following command, ::

        $ cd /s3-data/white-lab-hirak/data
        $ ls

Or alternatively you can use the following command to see the contents of the ``/s3-data/white-lab-hirak/data`` ::

        $ ls /s3-data/white-lab-hirak/data

*How to copy data from the server? (using GUI)*
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**windows**
For transferring files from and to the server you can use softwares such as
`CyberDuck <https://cyberduck.io/>`_, `WinSCP <https://winscp.net/eng/index.php>`_ or
`Filezilla <https://filezilla-project.org/>`_ or  `Bitvise SSH Client <https://www.bitvise.com/ssh-client-download>` All are free.
The appearance, and how they work are slightly different.

**Mac**
For transferring files from and to the server you can use softwares such as
`CyberDuck <https://cyberduck.io/>`_, `Filezilla <https://filezilla-project.org/>`_ .
Both are free. The appearance, and how they work are slightly different.


*How to copy data from the server? (from command line)*
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For advanced users using mac/linux machine can you the following command to copy
data from the server.

**Copying data _from_ remote**
Using rsync::

        rsync -av --progress <NetID>@wlab.cinj.rutgers.edu:<path_to_dir_to_copy> <your_local_dir>

*OR*
Using scp::

        scp -r <NetID>@wlab.cinj.rutgers.edu:<path_to_dir_to_copy> <your_local_dir>

**Copying data _to_ remote**
Using rsync::

        rsync -av --progress <your_local_dir> <NetID>@wlab.cinj.rutgers.edu:<path_to_dir_to_copy>

*OR*
Using scp::

        scp -r <your_local_dir> <NetID>@wlab.cinj.rutgers.edu:<path_to_dir_to_copy>


.. _IT website: https://it.rutgers.edu/virtual-private-network/
.. _VPN: https://it.rutgers.edu/guides/remote-access-with-anyconnect-virtual-private-network/


*Things to remember*

- You need to be connected to the VPN to access the server.
- **NEVER** use the ``sudo`` command unless you are absolutely sure what you are doing.
- **NEVER** delete any data from the server unless you are absolutely sure what you are doing. If you are not sure, ask Wenping Yang via teams.