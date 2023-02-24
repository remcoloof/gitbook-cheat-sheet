# Removing files

Sometimes we accidentally push sensitive data, such as a .env file. These files can be removed from the repository's history using BFG Repo-Cleaner.

{% hint style="danger" %}
Please note that you should consider sensitive data that is pushed to version control as compromised and it is best practice to rotate your secrets.
{% endhint %}

## Instructions

First, download the .jar file of BFG Repo-Cleaner at their [homepage](https://rtyley.github.io/bfg-repo-cleaner/). Once downloaded move to file to the root of your project and name. Then run the following command:

```
java -jar bfg.jar --delete-files .env
```

Make sure that you have a version of Java installed and that you use the right file name, i.e. substitute `bfg.jar` with the right file name. Thereafter, the file is removed and you must force push your changes. This may overwrite commits that other people have based their work on. To do so run the following command:

```
git push --force
```

This should remove the sensitive files from your repository. Please make sure that this is actually the case.

## Resources

* [https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
* [https://rtyley.github.io/bfg-repo-cleaner/](https://rtyley.github.io/bfg-repo-cleaner/)
