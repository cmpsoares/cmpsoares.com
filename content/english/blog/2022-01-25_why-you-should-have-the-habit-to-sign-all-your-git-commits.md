---
title: "Why you should have the habit to sign all your git commits"
date: 2022-01-25T17:00:00+00:00
# watermark text
watermark: "Tech Blog"
# page header background image
page_header_image: "https://user-images.githubusercontent.com/4914211/150984942-cf5809f3-2e40-438f-968e-1cd9973a5e95.png"
# meta description
description: "Why you should have the habit to sign all your git commits. And an easy to follow how-to on its configuration."
# post image
image: "https://user-images.githubusercontent.com/4914211/150984942-cf5809f3-2e40-438f-968e-1cd9973a5e95.png"
# post author
author: "Carlos Manuel Soares"
# post categories
categories: ["Developer Experience", "Cybersecurity", "Tutotial"]
# post tags
tags: ["git", "github", "gitlab", "security", "cybersecurity", "signature", "GPG", "cryptography", "how-to", "commit"]
# type
type: "post"
license: <a rel=\"license external nofollow noopener noreffer\" href=\"https://creativecommons.org/licenses/by-nc/4.0/\"
  target=\"_blank\">CC BY-NC 4.0</a>
comment: true
medium_repost_url: "https://medium.com/cmpsoares/why-you-should-have-the-habit-to-sign-all-your-git-commits-add2edef0135"
---
## It just looks so darn cool!

Even if you don't understand yet how and why you should sign Git commits, you might have seen this badge on GitHub:

![Github Verified Badge image](https://user-images.githubusercontent.com/4914211/150985482-c0fe167f-de38-4030-89b4-16b46b6a512e.png)


And even if you don't care about the security and authentication it provides to you and the community... How darn cool does that look! 😎

It sounds more challenging than it is, and you can set it up once, and you're good to go for ages! Until you format or destroy your PC, basically... Or if you buy a new one for the fifth time this year, you spoiled rich ba... Ahem! Let me get my composure back. How cool does that badge look, right?!


## But why should I sign anything anyway?

Well, before going into the how let's discuss the why. And no, it's not just about the green verified badge in Github...

For centuries we have been very creative in finding ways to mark or "sign" documents, tools, art as proof of identity, authenticity and intent. Naturally, the harder it is to replicate, the better. These can be written, stamped, mechanical, engraved and digital.

But why? Well, you might want to let people be assured that what they're reading, buying or using is really from you. You created it, and it wasn't someone impersonating you with any fraudulent intent.

At the beginning of the digital world, often it was considered enough to add a signature block to your content. Which is a block of text containing the author's name and contacts, and in some scenarios, images, ASCII art, usage licenses or disclaimers.

However, this is easier to copy and falsify than a handwritten signature... So good attempt, but sorry, it ain't gonna work...

This brings use to Digital or Cryptographic Signatures. Cryptographic digital signatures use public-key cryptography algorithms, also called asymmetric cryptography algorithms, to provide data integrity. This system uses a pair of text-based keys (a public and a private one). Essentially the private key is used to sign a document, and the public key is provided to the other party to verify your signature.

It's kind of like sending a glass box with a letter in it. You are the only one that can open the box and put the letter in it with the private key, everyone can read the letter in the box as it is made from glass, and those with your public key can use it to check if it is really your box.

There are many asymmetric cryptography algorithms for many use cases (even bitcoin and most cryptocurrencies are based on these). Still, for messaging, usually, GPG and S/MIME are the choices. The same goes for GitHub commit messages. GPG is generally considered the standard to sign text messages, and S/MIME has shown some strengths with email and other media that's not just text.


## So, how do we sign a commit anyway?

In short, you use a GPG key that you have generated yourself to sign the commits in practice and provide Github with the key's public counterpart.

GitHub then uses OpenPGP libraries to confirm that your locally signed commits and tags are cryptographically verifiable against one of the public keys you have added to your Github account.

To sign commits using GPG and have those commits verified on Github, we need to follow these simple steps:

1. Check for existing GPG keys
2. Generate a new GPG key
3. Add a new GPG key to your GitHub account
4. Tell Git about your signing key
5. Sign commits
6. Sign tags


### Part 1: Check for GPG installation and Keys

We will sign our commits using GPG based keys, so it is essential to validate if the tool is installed:

1. Open a Terminal
2. Run `which gpg` to verify if it is installed
3. If it has not been installed, as GPG does not come installed by default on macOS or Windows, we need to install the GPG command-line tools; see [GnuPG's Download page](https://gnupg.org/download/).
4. When installed, run the command `gpg --list-secret-keys --keyid-format=long` to list the long-form GPG keys for which you have both public and private keys. If this doesn't work, it might be that you're installation requires you to use `gpg2` instead, and you can run `gpg2 --list-keys --keyid-format LONG` (If you're using GPG2, you will correspondingly need to configure Git to use GPG2 with the command `git config --global gpg.program gpg2`)
5. Check the command output to see if you have a GPG key pair.
    * If there are no GPG key pairs or you don't want to use any available for signing commits and tags, go to the next step.
    * If there's an existing GPG key pair and you want to use it to sign commits and tags, then skip to step 3.

### Part 2: Generate a GPG key

Now we need to generate our GPG key to sign our commits with the following steps:

1. Generate a GPG key pair. As there are multiple versions of GPG, you should check the relevant `gpg` or `gpg2` [_man page_](https://en.wikipedia.org/wiki/Man_page) to find the appropriate key generation command. Your key must use RSA.
    - If you are on version 2.1.17 or greater, use the command below to generate a GPG key pair.
      ```shell
      $ gpg --full-generate-key
      ```
    - If you are not on version 2.1.17 or greater, the `gpg --full-generate-key` command doesn't work. Instead, paste the command below and skip to step 6.
      ```shell
      $ gpg --default-new-key-algo rsa4096 --gen-key
      ```
2. At the prompt, specify the kind of key you want or press `Enter` to accept the default.
3. Set the key size you desire or press `Enter` to use the default value at the following input. Your key needs to be at least `4096` bits.
4. Enter the key's time to live or press `Enter` to specify the default selection, indicating that the key doesn't expire.
5. Confirm that your selections are correct.
6. Enter your user ID information. When requested to enter your email address, ensure that you enter a verified email address for your GitHub account. You can use the comment field to add your company name if desired.
7. Type a secure passphrase.
8. Now use the `gpg --list-secret-keys --keyid-format=long` command to validate that it has been created successfully.


### Part 3: Adding the GPG key to Github:

For Github to know if the key is yours, we need to add the public key to your account (In case you wish to set this up on Gitlab, the steps to do in their web app are very similar, and I would recommend looking into [this part of their documentation](https://docs.gitlab.com/ee/user/project/repository/gpg_signed_commits/#adding-a-gpg-key-to-your-account)):

1. Open a Terminal
2. Use the `gpg --list-secret-keys --keyid-format=long` command to list the long form of the GPG keys for which you have both the public and private keys. The private key is required for signing commits or tags.
3. From the GPG key list, copy the long form of the key ID you'd like to use. In this example, the GPG key ID is `AFBBCB53E2D934D5`:
```shell
$ gpg --list-secret-keys --keyid-format=long
/Users/cmpsoares/.gnupg/pubring.kbx
-----------------------------------
sec   rsa4096/AFBBCB53E2D934D5 2021-10-11 [SC]
      F30FB917267E70CD6A8C3A57AFBBCB53E2D934D5
uid                 [ultimate] Carlos Manuel Soares (CMPSoares Lda.) <carlos@cmpsoares.com>
ssb   rsa4096/C744C29A059EAE08 2021-10-11 [E]
```
4. Paste the command below, substituting the GPG key ID you'd like to use. In this example, the GPG key ID is `AFBBCB53E2D934D5`:
  ```shell
  $ gpg --armor --export <em>AFBBCB53E2D934D5</em>
  # Prints the GPG key ID, in ASCII armor format
  ```
5. Copy your GPG key, beginning with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with `-----END PGP PUBLIC KEY BLOCK-----`.
6. Go to your browser and log in to your account on github.com
7. In the upper-right corner of any page, click your profile photo, then click **Settings**.
  <br><img src="https://user-images.githubusercontent.com/4914211/151029896-fc9bd04e-d58b-4f30-83d8-03caa24ee605.png" alt="Settings icon in the user bar" width="200">
8. Click on **SSH and GPG keys**.
  <br><img src="https://user-images.githubusercontent.com/4914211/151030515-b789b392-6396-4441-b5a1-def1350856a9.png" alt="Authentication keys" width="250">
9. Click the **New GPG key** button.
   <br><img src="https://user-images.githubusercontent.com/4914211/151030850-c6ab0641-c989-4e78-85c1-9c060af6073f.png" alt="GPG Key Button" width="750">
10. In the "Key" field, paste the GPG key you copied when you generated your GPG key.
   <br><img src="https://user-images.githubusercontent.com/4914211/151031140-b1c86529-4f96-4b37-a00e-da77bf3a9c7a.png" alt="The key field" width="750">
11. Click the **Add GPG key** add.
   <br><img src="https://user-images.githubusercontent.com/4914211/151031415-83f241bc-eb33-4295-b591-d0eb7557a603.png" alt="The Add key button" width="150">
12. To confirm the action, you may be prompted to enter your GitHub password.


### Part 4: Configuring `git` to use your signature

So now that you have a GPG keypair ready, we need to tell Git to use it whenever we need to sign a commit or a tag:

1. Open Terminal.
2. With the `gpg --list-secret-keys --keyid-format=long` command, we list the long form of the GPG keys for which you have both a public and private key. A private key is required for signing commits or tags.
3. Copy the long form of the GPG key you would like to use from the list of keys. In this example, the GPG key ID is `AFBBCB53E2D934D5`:
```shell
$ gpg --list-secret-keys --keyid-format=long
/Users/cmpsoares/.gnupg/pubring.kbx
-----------------------------------
sec   rsa4096/AFBBCB53E2D934D5 2021-10-11 [SC]
      F30FB917267E70CD6A8C3A57AFBBCB53E2D934D5
uid                 [ultimate] Carlos Manuel Soares (CMPSoares Lda.) <carlos@cmpsoares.com>
ssb   rsa4096/C744C29A059EAE08 2021-10-11 [E]
```
4. To set your GPG signing key in Git, paste the command below, substituting in the GPG key ID you'd like to use. In this example, the GPG key ID is `AFBBCB53E2D934D5`:
```shell
$ git config --global user.signingkey AFBBCB53E2D934D5
```
***Note that you might need to repeat this step when you clone new git repositories to your machine.***
5. To add your GPG key as an environment variable by setting the following command in your terminal profile (depending on the terminal that you use, this can vary, but it's usually a `.profile`, `.<terminal_being_used>_profile` or `.<terminal_being_used>` file in your HOME or ROOT folder. In my case, it is `~/.zshrc`, so you can add your GPG like this:
```shell
$ echo 'export GPG_TTY=$(tty)' >> ~/.zshrc
```


### Part 5: Sign the commits by default (Optional)

Naturally, as you now have configured the GPG key, you can now sign your commits by adding the `-S` flag to your commit command, and it will prompt you for the passphrase and sign the commit, but this can also be set as default.

To configure your Git client to sign commits by default for a local repository, in Git versions 2.0.0 and above, run the command `git config commit.gpgsign true`. To set this as default in any local repository on your machine, run it with the `--global` flag like this: `git config --global commit.gpgsign true`.

***Note that you might need to repeat this step as well when you clone new git repositories to your machine.***

To store your GPG key passphrase, so you don't have to enter it every time you sign a commit, we recommend using any of the following tools:

 * For Mac users, the GPG Suite allows you to store your GPG key passphrase in the Mac OS Keychain.
 * For Windows users, the Gpg4win integrates with other Windows tools.

You can also manually configure the gpg-agent to save your GPG key passphrase, but this doesn't integrate with Mac OS Keychain like ssh-agent and requires more setup.


### Part 6: Sign old commits

You might want to re-sign your old commits for compliance in some scenarios. An example of this is that more corporations only allow fully certified/signed Actions to be used from the GitHub Actions Marketplace. Another is that as a Software Developer, you might want to prove that it was really you that provided a piece of code. Having all your code signed makes it easier for others to trust you. Which is very useful and sometimes even required when contributing to Open-source projects. So if you're in a situation where all the code you have to deliver must be signed to be compliant, you might need to re-sign all your commits with the following steps:
1. Open a Terminal
2. Go to your project repository
3. Make sure your local branch is up-to-date
4. Run the following command:
```shell
git rebase --exec 'git commit --amend --no-edit -n -S' -i <oldest_rev or --root if it is the whole repo>
```
5. If you need to sign the root commit, there are situations where you also need to use the following commands:
```shell
git checkout <root_commit_sha>
git commit --amend -S
# Don't change anything and save/close vi
git rebase --onto HEAD <root_commit_sha> main
```
5. Then force push to Github: `git push --force`

All your commits should be signed by this time, and in Github, they will show that cool Verified Badge.

![Github Verified Badge image](https://user-images.githubusercontent.com/4914211/150985482-c0fe167f-de38-4030-89b4-16b46b6a512e.png)

But more important than that, you ensure the people consuming your code know that it is really yours, thus adding that professional flair to it.


<details>
<summary>
<a class="btnfire small stroke">References</a>    
</summary>
<ul>
    <li><a href="https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key">Generating a new GPG key - GitHub Docs</a></li>
    <li><a href="https://docs.gitlab.com/ee/user/project/repository/gpg_signed_commits/#adding-a-gpg-key-to-your-account">GPG Signed Commits - GitLab Docs</a></li>
</ul>
</details>
