pipeline {
    agent any
    stages {
        stage('Build') {
	    environment {
                CONFLUENCE_CREDS=credentials('katsdpdocstest')
            }
            steps {
                sh '''#!/bin/bash
		  FILES=($(git show --name-only --diff-filter=ACMRT | grep '.md$'))
		  echo "Processing files for possible Confluence upload: $FILES"
			
		  if [[ "${#FILES[@]}" == "0" ]]; then exit 0; fi;
		  set -e;
		  for file in ${FILES[@]}; do
		    echo;
		    echo "> Uploading ${file}";
		    CID=`docker create --rm -i kovetskiy/mark:latest -l https://skaafrica.atlassian.net/wiki -u CONFLUENCE_CREDS_USR -p CONFLUENCE_CREDS_PSW -f ${file}`
		    docker cp ${file} $CID:/docs/
		    docker start -a -i $CID
		  done
                '''
            }
        }
    }
}
