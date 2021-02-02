Storage
=======

It is important to know the different storage options available in litio, since
not all of them serve the same purposes.

.. hint::

   Find out where you are with ``pwd``

/home
"""""
**Backup:** yes

**Limit:** yes (300Gb/user)

That is where you are when you log in (/home/user). Everything stored here is
backed up. Since the backup space is limited, each user's is limited to 3Gb.

/scratch
""""""""
**Backup:** no

**Limit:** no per-user limit (total ~4Tb)

Intended to execute calculations. Specially important when this calculations
demand a lot of disk space. The script described in :ref:`script` already takes 
care of executing everything in the */scratch* directory.


/data
"""""
**Backup:** no

**Limit:** no per-user limit (total ~8Tb)

Store here your large files. Be aware that the information stored here is not backed up.
