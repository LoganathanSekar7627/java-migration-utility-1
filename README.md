# java-migration-utility
Java Migration utility from Java 11 to Java 21. 
Use this utility that will be useful in making 
* pom version changes,
* Java package changes to the java files,
* docker file changes and push trigger file changes. 

Refer file for the [text_changes.py](text_changes.py) done in the utility.  This needs python 3.

## Steps
1. Configure the migration_config.py with correct `git_base_dir` and `modules_paths_list_in_order`.
2. Run command to apply the textual changes mentioned.
````
python java-migration-utility.py --migrate
````

### Note: 

1. The changes needed to be done for adding the `kernel-bom` is not included.
2. The changes needed to be done on the deprecated APIs are not included in this utility, which needs to be done additionally.

## Usage:
````
usage: java-migration-util.py [-h] [--gitBaseDir GIT_BASE_DIR]
                              [--listModules]
                              [--listGitRepos]
                              [--startIndex [START_INDEX]] [--index [INDEX]]
                              [--migrate]
                              [--fetchMerge] [--status]
                              [--diff]
                              [--mvnCleanInstall]
                              [--mvnCleanInstallSkipTests]
                              [--addCommitAndPushToOrigin]
                              [--add] [--commit]
                              [--commitMessage COMMIT_MESSAGE]
                              [--pushToOrigin]

options:
  -h, --help            show this help message and exit
  --gitBaseDir GIT_BASE_DIR, -gbd GIT_BASE_DIR
                        Git Base Directory
  --listModules, -lsm
                        List Modules
  --listGitRepos, -lsr
                        List Git Repos
  --startIndex [START_INDEX], -si [START_INDEX]
                        The start index of module from which build to start
  --index [INDEX], -i [INDEX]
                        The index of module from which specifically needs to
                        be built
  --migrate, -mig
                        Migrate
  --fetchMerge, -fm
                        Fetch upstream and merge develop-java21 branch
  --status, -st
                        git status on all modules
  --diff, -df
                        git diff on all modules
  --mvnCleanInstall, -mci
                        Maven Clean Install
  --mvnCleanInstallSkipTests, -mcist
                        Maven Clean Install with Skip tests and javadoc in
                        build
  --addCommitAndPushToOrigin, -acp
                        Add changes, commit and push to origin
  --add, -ad
                        Add changes
  --commit, -cm
                        Commit
  --commitMessage COMMIT_MESSAGE, -m COMMIT_MESSAGE
                        Commit and push to origin
  --pushToOrigin, -po
                        push to origin

````

* This utility allows to do batch maven build so that the maven build is done in batch for all modules together in the order of the dependencies defined in the migration_config.py file. For example, python java-migration-utility.py `--mvnCleanInstall`. It also has options such as `--mvnCleanInstallSkipTests` , `--listModules` , `--listGitRepos` , `--startIndex [start-index]` and `--index [index]`.
* This also has git based options that will run together for all repositories together such as `--status`, `--diff`, `--add` , `--commit` ,  `--commitMessage`,  `--pushToOrigin`  and `--addCommitAndPushToOrigin`.You may need to configure branch in the text_changes.py file for this.
* For windows users, if you are having gitbash, you can run the python script with that which will enable using the batch commit and push of multiple repositories and modules.
