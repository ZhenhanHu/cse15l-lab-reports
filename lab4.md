# **Lab Report 4 -- Zhenhan Hu(A17282448)**
---
# **Step 4**
![Image](/images/report4-images/step4_ssh_login.png) <br>
I first Logged into my `ieng6` account using `ssh`. <br>
Keys pressed: `ssh` `<space>` `zhh039@ieng6-201.ucsd.edu`  `<enter>`

# **Step 5**
![Image](/images/report4-images/step5_git_clone.png) <br>
I have the `SSH` URL, `git@github.com:ZhenhanHu/lab7.git`, for the forked repository from GitHub copied to my clipboard by pressing `<Command + C>`, then cloned it. <br>
Keys pressed: `git` `<space>` `clone` `<space>` `<Command + V>` `<enter>`

# **Step 6**
![Image](/images/report4-images/step6_tests_failed.png) <br>
After changing the current working directory to `lab7`, I ran the tests demonstrating that they failed. 
Note: Key pressed `<tab>` helped me fill in the rest of the repository/file name: `l` for `lab7/` and `t` for `test.sh`. <br>
Keys pressed: `cd` `<space>` `l` `<tab>` `<enter>`, and then `bash` `<space>` `t` `<tab>` `<enter>`

# **Step 7**
![Image](/images/report4-images/step7.1_vim.png) <br>
![Image](/images/report4-images/step7.2_fix.png) <br>
I opened the Vim text editor to edit and fix the file in order to pass the tests. Again, pressing `<tab>` after `L` and adding `.java` enters the file name completely. <br>
Keys pressed: `vim` `<space>` `<Shift + L>` `<tab>` `.java` `<enter>`

The instruction to fix the code specifies changing `index1` to `index2`  on the line where the command is indicated. So, I first find "index1" using `/index1` and `<enter>` to confirm
my choice, and then using `n` to go through each matched option until the one I need to fix. Then, After reaching the last character at the end of the word, "1", using `e` and 
replacing it with "2", using `r`, I pressed `<Esc>` to go back to the normal mode. After that, I typed `:wq` to save and quit the file, and pressed `<enter>`. <br>
Keys pressed(vim): `/index1` `<enter>` `n` `n` `n` `n` `n` `n` `n` `n` `n` `e` `r` `2` `<Esc>` `<Shift + ;>` `wq` `<enter>`

# **Step 8**
![Image](/images/report4-images/step8_tests_succeed.png) <br>
After fixing the code, I reran the tests, which should all be passed. Again, pressing `<tab>` helps me fill in the rest of `test.sh`. <br>
Keys pressed: `bash` `<space>` `t` `<tab>` `<enter>`

# **Step 9**
![Image](/images/report4-images/step9_commit_push.png) <br>
Lastly, I committed and pushed the resulting change to my Github account with the commit message "Update". Specifically, I first used `git add` with the file to stage changes for 
the next commit, then used `git commit` to save my staged changes with `-m` to include my commit message, and lastly, I used `git push origin main` to send the committed changes 
to my GitHub account. <br>
Keys pressed: `git` `<space>` `add` `<space>` `<Shift + L>` `<tab>` `<enter>`, and then `git` `<space>` `commit` `<space>` `-m` `<space>` `<Shift + '>` `<Shift + U>pdate` `<Shift + '>` `<enter>`,
and lastly `git` `<space>` `push` `<space>` `origin` `<space>` `main` `<enter>`

