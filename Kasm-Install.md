*   The Default usernames are **admin@kasm.local** and **user@kasm.local**. The passwords will be randomly generated and presented at the end of the install unless the `--admin-password` or/and `--user-password` are specified.

# **Admin** **Account Recovery**[****](https://www.kasmweb.com/docs/latest/how_to/admin_account_recovery.html#admin-account-recovery)

**Admin**s may find themselves locked out of their accounts by forgetting or mis-setting their account passwords. This guide will show show the steps for resetting the admin account password.

1.  SSH to the **Kasm** Workspaces server and connect to the database with the following command:
    
    > sudo docker exec \-it **kasm**\_db psql \-U **kasm**app \-d kasm
2.  Reset the **Admin** password, clear WebAuthn credentials, clear TOTP credentials and exit the psql shell
    
    > update users set
    >     pw\_hash \= 'fe519184b60a4ef9b93664a831502578499554338fd4500926996ca78fc7f522',
    >     salt \= '83d0947a-bf55-4bec-893b-63aed487a05e',
    >     secret\=NULL, set\_two\_factor\=False, locked\=False,
    >     disabled\=False, failed\_pw\_attempts \= 0 where username \='**admin**@**kasm**.**local**';
    > DELETE FROM webauthn\_credentials WHERE user\_id IN ( SELECT user\_id FROM users WHERE username \= '**admin**@**kasm**.**local**' );
    > **\\q**
3.  Login to the Workspaces UI using “**admin**@**kasm**.**local**” with the password “password” and reset your password to a secure password.

<img class="image_resized" style="aspect-ratio:1054/625;height:auto;width:auto;" src="api/attachments/t3D8ATNiwsaV/image/password_change.webp" alt="../_images/password_change.webp" width="1054" height="625">

<figure><p style="margin-left:0px;"><em><strong>Reset Password Location</strong></em><a href="https://www.kasmweb.com/docs/latest/how_to/admin_account_recovery.html#id1"></a></p></figure>