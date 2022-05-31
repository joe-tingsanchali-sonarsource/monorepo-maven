node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    when {
      anyOf {
        changeset 'module1/src/main/**'
        changeRequest()
      }
    }
    def mvn = tool 'Default Maven';
    withSonarQubeEnv('local89') {
      sh """
        ${mvn}/bin/mvn clean verify -X sonar:sonar \\
          -Dsonar.projectKey=monorepo-maven-mod1 \\
          -Dsonar.projectName=monorepo-maven-mod1 \\
          -Dsonar.inclusions=module1/src/main/** \\
          -Dsonar.test.inclusions=module1/src/test/**
      """
    }
  }
}
