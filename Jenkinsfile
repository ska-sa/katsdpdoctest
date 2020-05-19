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
		  echo `pwd`
		  echo `ls`
		  if [[ "${#FILES[@]}" == "0" ]]; then exit 0; fi;
		  set -e;
		  for file in ${FILES[@]}; do
		    echo;
		    echo "> Uploading ${file}";
		    docker run --rm -i -v=`pwd`:/docs kovetskiy/mark:latest -l https://skaafrica.atlassian.net/wiki -u CONFLUENCE_CREDS_USR -p CONFLUENCE_CREDS_PSW -f ${file};
		  done
                '''
            }
        }
    }
}
