node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def mvn = tool 'Default Maven';
    withSonarQubeEnv('ee89') {
      sh """
        ${mvn}/bin/mvn clean verify sonar:sonar \\
          -Dsonar.projectKey=monorepo-maven-mod1 \\
          -Dsonar.projectName=monorepo-maven-mod1 \\
          -Dsonar.inclusions=module1/src/main/** \\
          -Dsonar.test.inclusions=module1/src/test/**
      """
    }
  }
}
