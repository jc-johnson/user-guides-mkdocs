# How to Merge Branches in TortoiseGit

The task of merging branches where separate features are developed
and combining them into the main branch is an essential part of using
Git. TortoiseGit is a helpful GUI for managing a Git project. It provides a
simple interface for complex operations such as merging branches.

## Merging in TortoiseGit

There are two primary ways of merging branches in TortoiseGit:

### Method 1 - Merge another branch into the current branch
1. In File Explorer navigate to your Git repo location and right-click on the repository directory. 
2. Ensure you have checked out the branch that you want to merge changes into.   
3. In the context menu navigate to **TortoiseGit > Merge**.
4. In the following window under **From > Branch** select the branch you want merged into the current branch. 
5. Click **OK**.

### Method 2 - Merge when Switching Branches
In TortiseGit you can choose which branch you want to merge when switching branches.

1. In File Explorer, right-click on the repository directory. 
2. Select **TortoiseGit > Switch/Checkout**.
3. Under **Switch To** select the branch you want to merge changes into.
    - For example, if you want to merge changes from **FEATURE-BRANCH-ONE** into **MAIN** branch, check out the **MAIN** branch. 
4. In the window that notifies you the checkout has been successful, click **Merge**.
    - **Note:** You may need to stash any unpublished changes or resolve merge conflicts before you are able to switch to another branch.
5. In the Merge window under **From > Branch** select the branch you wish to merge into the current branch.
6. Click **OK**.