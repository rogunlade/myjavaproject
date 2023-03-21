# myjavaproject
-12,6 +12,15 @@ steps:
          download: "target/*.jar"
  - label: "Push Image"
    command: "docker push rogunlade/myjavaproject:latest"
  - label: "Create Secret"
    env:
      PATH: "$PATH:/var/lib/buildkite-agent/apache-maven-3.6.3/bin:/var/lib/buildkite-agent:/usr/local/bin"
      AWS_PROFILE: "buildkite"
    commands:
      - "git clone git@github.com:rogunlade/GKE-deployment-files.git"
      - "cd GKE-deployment-files/java"
      - "kubectl create secret generic javaapp --from-literal=SQL_PASSWORD=kihtrak -n javaproject"
    if: build.message =~ /secret/
  - label: "Deploy"
    env:
      PATH: "$PATH:/var/lib/buildkite-agent/apache-maven-3.6.3/bin:/var/lib/buildkite-agent:/usr/local/bin"
