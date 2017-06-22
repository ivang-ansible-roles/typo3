# Scenario

1. Validate variables and check host system
    1. Check if domain name(`typo3_domain_name` variable) is set, and fail if not
    1. Check if site root folder(`typo3_root`) is set and the destination folder don't exists or is empty, and fail otherwise
    1. Check if database name(`typo3_db_name` variable) is set and valid, and the target db don't exists or is empty, and fail otherwise
    1. Check if database user(`typo3_db_user` variable) is set and valid, and fail otherwise
    1. Check db user password(`typo3_db_password` variable, it can be an empty string), if not set then:
        1. check if the file `/tmp/${typo3_db_user}-${typo3_db_name}` exists
        1. if not then generate a random password and store it in the file `/tmp/${typo3_db_user}-${typo3_db_name}`
        1. load the password from the file `/tmp/${typo3_db_user}-${typo3_db_name}`(regardless, new or old)
        1. store it in the role variable `typo3_db_password` for further use
        1. print the password in the console
1. Create the db
1. Create db user with specified password and all privileges for the db
1. Copy the TYPO3 Distribution into the destination folder
1. Run `composer install` inside the destination folder
1. Bootstrap TYPO3 with `typo3cms install:setup`
1. Create the nginx vhost
