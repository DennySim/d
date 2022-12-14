// Example usage
node {
    /** git url: 'https://github.com/jenkinsci/git-tag-message-plugin'  */
    /** git url: 'https://github.com/DennySim/d'  */
    env.GIT_TAG_NAME = gitTagName()
    /** env.GIT_TAG_NAME = "COOLTAG" */
    /** env.GIT_TAG_MESSAGE = gitTagMessage()  */
    
    
    stage("Git checkout"){
        git branch: 'main', url: 'https://github.com/DennySim/d'
    }
    if (env.GIT_TAG_NAME=='null'){
        stage("ECHO COOL APP"){
            dir('terraform'){
                sh 'echo COOLAPP-step-01'
                sh "echo ${env.GIT_TAG_NAME}"
                sh 'echo COOLAPP-step-02'
            }
        }  
    }    
    else{
        dir('terraform'){
            sh 'echo NOTCOOLAPP'
            sh "echo ${env.GIT_TAG_NAME}"
        }
    }
    
}

/** @return The tag name, or `null` if the current commit isn't a tag. */
String gitTagName() {
    sh "echo DIPLOMAWORK_00"
    commit = getCommit()
    if (commit) {
        sh "echo DIPLOMAWORK_01"
        desc2 = sh(script: "echo DIPLOMAWORK_02")
        desc = sh(script: "git describe --tags ${commit}", returnStdout: true)?.trim()
        sh "echo DIPLOMAWORK_03"
        sh "echo TAG ${desc}"
        sh "echo DIPLOMAWORK_04"
        if (isTag(desc)) {
            return desc
        }
    }
    return null
}

/** @return The tag message, or `null` if the current commit isn't a tag. */
String gitTagMessage() {
    sh "echo DIPLOMAWORK_05"
    name = gitTagName()
    msg = sh(script: "git tag -n10000 -l ${name}", returnStdout: true)?.trim()
    if (msg) {
        return msg.substring(name.size()+1, msg.size())
    }
    return null
  }

String getCommit() {
    return sh(script: 'git rev-parse HEAD', returnStdout: true)?.trim()
}

@NonCPS
boolean isTag(String desc) {
    match = desc =~ /.+-[0-9]+-g[0-9A-Fa-f]{6,}$/
    result = !match
    match = null // prevent serialisation
    return result
}
