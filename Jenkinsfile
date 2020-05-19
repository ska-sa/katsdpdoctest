pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
		  FILES=($(git show --name-only --diff-filter=ACMRT | grep '.md$'))
		  if [[ "${#FILES[@]}" == "0" ]]; then exit 0; fi;
		  set -e;
		  for file in ${FILES[@]}; do
		    echo;
		    echo "> Uploading ${file}";
		    docker run --rm -i -v=$(pwd):/docs kovetskiy/mark:latest -u broken_username@ska.ac.za -p broken_password -f ${file};
		  done
                '''
            }
        }
    }
}
