Account Setup
=============

Setting up a new email account? Here’s what all the settings do.

☠️ **But first, a word of warning!**
The import process does things you might not expect:

.. danger:: 🚯 **Zammad will delete all emails in your inbox
   during the import process.**

   Use the *Experts* dialog to
   :ref:`disable this behavior <email-experts-keep-messages-on-server>`.

   .. _email-experts-import-as-warning:

.. warning::

   📮 **Zammad will send an auto-reply message to every email it imports.**
   (Including the old ones!)

   Use the *Experts* dialog to
   :ref:`change this behavior <email-experts-import-as>`.

.. note::

   **Gmail / G Suite users:**
      Google is in the process of upgrading its security policies.
      To stay up-to-date, do **not** add your account as an email
      channel — instead, create a
      :doc:`Google channel </channels/google/accounts/account-setup>`.

   **Microsoft 365 users:**
      Microsoft is in the process of upgrading its security policies.
      To stay up-to-date, do **not** add your account as an email
      channel — instead, create a
      :doc:`Microsoft 365 channel </channels/microsoft365/accounts/account-setup>`.

Basic
-----

In most cases, Zammad is smart enough
to figure out your email provider’s configuration
based on your email address alone.

.. figure:: /images/channels/email/accounts-new-success.gif
   :alt: Enter your email address and password, and Zammad will figure out the
         rest.
   :scale: 50%
   :align: center

Organization & Department Name
   The display name used for outgoing email.

   .. figure:: /images/channels/email/account-setup-org-dept-name.png
      :alt: Screenshot of customer inbox with email from "Chrispresso Sales"
      :scale: 40%
      :align: center

      A customer’s inbox with an auto-reply from **Chrispresso Sales**.

   If you add :doc:`multiple addresses <secondary-addresses>` to a single
   account, you can define a separate Organization & Department Name for each
   one.

   Email display names value can be
   :ref:`further customized in the Settings tab <email-settings-sender-format>`.

Email
   Your email address.

   If your account login/username is different from your email address,
   use the *Experts* dialog (see below).

   If your inbox receives mail for more than one email address,
   be sure to :doc:`add your alternate addresses <secondary-addresses>`
   after account setup.

Password
   Your account password.

Destination Group
   The :doc:`group </manage/groups/index>` that incoming mail will be assigned
   to.

   Use :doc:`filters </channels/email/filters>` for more fine-grained sorting
   of incoming email.

.. _email-new-account-experts:

Experts
-------

If Zammad can’t figure out how to connect your account
(or if you just want to access advanced settings),
use the *Experts* dialog.

.. figure:: /images/channels/email/accounts-new-failure.gif
   :alt: When auto-detection fails, you will be presented with the "Experts"
         account setup dialog.
   :scale: 50%
   :align: center

Email Inbound
^^^^^^^^^^^^^

Type
   Choose from **IMAP** and **POP3**.

   In most cases, you want IMAP.
   (With POP3, you won’t be able to
   :ref:`keep messages on the server <email-experts-keep-messages-on-server>`
   or :ref:`specify which folder to fetch from <email-experts-folder>`.)

Host
   Your email server’s hostname or IP address (*e.g.,* ``imap.gmail.com``).

   Contact your email provider or system administrator if you don’t know.

User
   This field is being pre-filled with your email address in case you've
   provided one before opening the expert settings.

   Adjust this setting in case your username and email address differ.

Password
   Your account password.

SSL / STARTTLS
   Enable encryption when fetching messages.

   You can choose from the following options:

      * No SSL

        .. warning::

           Retrieving Emails, just like sending your
           username and password without any encryption *is not secure*.

           You should never use this configuration on internet machines!

      * SSL
      * STARTTLS

Port
   Your email server’s port (usu. ``993`` for IMAP, or ``995`` for POP3).

   Contact your email provider or system administrator if you don’t know.

   .. _email-experts-folder:

Folder
   Specify which folder to fetch from, or leave empty to fetch from ``INBOX``.

   If specifying a nested folder, be sure to use the full path.
   (Some systems use different **path separators**;
   *e.g.,* ``Inquiries/Tech-Support`` vs. ``Inquiries.Tech-Support``.
   Contact your email provider or system administrator if you don’t know.)

   .. note:: 📥 **Additional Steps Required**

      In the last step of the account setup process,
      Zammad sends you an email from your own account,
      then waits for it to appear in the folder specified here.
      **Account verification will not complete until
      this test message has been received.**

      If this folder does not receive incoming messages automatically,
      you may have to manually check your inbox during the verification step
      and move Zammad’s test message there when it arrives.

   .. _email-experts-keep-messages-on-server:

Keep messages on server
   Specify what happens to your emails after Zammad imports them:

   * ``no`` Zammad deletes all imported messages

   * ``yes`` Zammad marks imported messages as read

     (With this option, Zammad will only import unread messages.
     This means Zammad may miss messages if the mailbox is externally modified.)

   .. note:: 🤔 **Why does Zammad delete messages by default?**

      If you never clean out your inbox,
      it’ll eventually reach its storage limit,
      and your mail server will start **rejecting incoming messages**.
      Most Zammad users never even look at their inbox once it’s set up,
      so they rely on Zammad to keep it clean for them.

      If you choose **yes** here, remember that it’s your responsibility
      to clean out your inbox from time to time
      to keep it below its storage limit.

   .. _email-experts-import-as:

Import as
   .. figure:: /images/channels/email/account-setup-archive-import.png
      :alt: “Import as” option in email account setup dialog
      :align: center
      :width: 40%

      How should old emails be imported?

   During the import process, Zammad treats **all messages**
   (including ones you’ve already read from months or years ago)
   as if they had been sent today:
   senders will receive auto-replies saying
   “your message has been received and we’ll get back to you within 24 hours,”
   and tickets created for each message will be marked as “new”.

   Use this option to disable this behavior for messages more than two weeks
   old.

   .. note:: This option may not be shown if:

      * all messages in your inbox are less than two weeks old
      * you selected **Keep messages on server: Yes**
      * you selected **Type: POP3**

      For more fine-grained control,
      manually disable this and other :doc:`triggers </manage/trigger>`
      before adding an email account,
      then turn them back on once all your messages have been imported.

Email Outbound
^^^^^^^^^^^^^^

Send mails via
   Choose from **SMTP** and **local MTA** (*e.g.,* Sendmail).

   Local MTA (mail transfer agent) configuration
   is only available on self-hosted installations.

Host
   Your email server’s hostname or IP address (*e.g.,* ``smtp.gmail.com``).

User
   Your account login/username.

   Leave blank to use the same value from incoming account setup.

Password
   Your account password.

   Leave blank to use the same value from incoming account setup.

Port
   Your email server’s port (usu. ``587`` or ``465``).

   Zammad will detect and enable SSL/STARTTLS support automatically.

Verification
------------

.. figure:: /images/channels/email/adding-email-account_verification-send-and-receive.gif
   :alt: Email account verification step
   :align: center

As a final step, Zammad sends a test email from your own account,
to your own account, and to ``verify-external-smtp-sending@discard.zammad.org``
which discards the test mail right away.

We've created a `landing page for discard.zammad.org`_ which describes the
backgrounds as well.

.. _landing page for discard.zammad.org:
   https://discard.zammad.org

This this Zammad ensures that your email account is capable of sending internal
and external - once this is verified the setup process is complete! 🎉

.. include:: /channels/email/accounts/account-setup-group-hint.include.rst

Troubleshooting
^^^^^^^^^^^^^^^

* :ref:`Is a custom incoming mail folder to blame? <email-experts-folder>`
