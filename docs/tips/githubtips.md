# GitHub Tips

## Procedural steps to make contributions

- Fork the project (done via website)
- Clone your fork (to your system)
- Run ``` git status ```
- Create a branch to work from ``` git checkout -b <branch-name> ```
- Check status ``` git status ```
- Make your code/changes/etc.
- Run ``` git add <file-name> <file-name> ```
- Commit your changes ``` git commit -m "appropriate note" ```
- Push your changes ``` git push ```
- Configure a remote for the fork ``` git remote add upstream https://github.com/original-owner-username/original-repository.git ```
- Update the latest version of the upstream to avoid conflicts ``` git fetch upstream ```
- Switch to main branch in your local fork ``` git checkout main ```
- Merge the upstream changes to your local main branch thus avoiding PR conflicts ``` git merge upstream/main ```
- Request a PR on GitHub (website) after you have done your changes.

## Learning more

- Use GitHub's learning tool <https://lab.github.com>
- Short helpful reads <https://guides.github.com>
- Digital Ocean Tutorial Series for Open Source <https://www.digitalocean.com/community/tutorial_series/an-introduction-to-open-source>
- Thanks to the opensourceTips page, we discovered this <https://learngitbranching.js.org>

## Extra

- Use [**SSH**](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh) where possible
