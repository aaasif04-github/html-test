// @Library('sds-common') _

def buildS3SourcePath   = "ps-sds-config/"
def projectName         = "paysafe"
def deploy_environment  = "dev"
def destinationPath     = "s3://test/"

properties([
    parameters([
        [$class: 'ChoiceParameter', 
            choiceType: 'PT_SINGLE_SELECT', 
            description: 'Select the Module', 
            filterLength: 1, 
            filterable: false, 
            name: 'ModuleName', 
            randomName: 'choice-parameter-3046005597044849', 
            script: [$class: 'GroovyScript', 
                fallbackScript: [
                    classpath: [], 
                    sandbox: false, 
                    script: 'return [\'Project Not available\']'
                ], 
                script: [
                    classpath: [], 
                    sandbox: false, 
                    script: 'return [\'Airflow\',\'AnalyticalJobs\',\'Airflow-v1\']'
               ]
            ]
        ],
        // [$class: 'ChoiceParameter', 
        //     choiceType: 'PT_SINGLE_SELECT', 
        //     description: 'Select the Build', 
        //     filterLength: 1, 
        //     filterable: false, 
        //     name: 'BUILD_VERSION', 
        //     randomName: 'choice-parameter-3046005597044848', 
        //     script: [$class: 'GroovyScript', 
        //         fallbackScript: [
        //             classpath: [], 
        //             sandbox: false, 
        //             script: 'return [\'Build Not available\']'
        //         ], 
        //         script: [
        //             classpath: [], 
        //             sandbox: false, 
        //             script: '''\
        //                 def command = "aws s3 ls  pai-management-artifactory/artifacts/dev/ps-sds-config/ --recursive| sort -r | head -10 | awk -F ps-sds-config \\\'{print \\\$2}\\\' | awk -F \\\'/\\\' \\\'{print \\\$2}\\\'"
        //                 def project = [\'bash\', \'-c\', command].execute()
        //                 project.waitFor()
        //                 return project.text.readLines()
        //             '''.stripIndent().trim()
        //        ]
        //     ]
        // ]
    ])
])

pipeline {
    agent any

    stages{
        stage ('printTheVariables') {
            steps{
                script {
                    println "${buildS3SourcePath}"
                    println "${ModuleName}"
                    println env.WORKSPACE
                    println "present working dir: " + pwd()
                }
            }
        }

        stage ('printhtml') {
            steps{
                script {
                    publishHTML ([allowMissing: false,
                        alwaysLinkToLastBuild: false,
                        keepAll: true,
                        reportDir: '',
                        reportFiles: 'myreport.html',
                        reportName: 'My Reports',
                        reportTitles: 'The Report'])
                }
            }
        }

        // stage ('setTheOutputVariables') {
        //     steps{
        //         script {
        //             if ("${ModuleName}" == 'Airflow'){
        //                 zipFileName         = "sds-config-airflow-v21"
        //                 outputPathPrefix    = "codebuild-orchestration"
        //             } else if ("${ModuleName}" == 'AnalyticalJobs'){
        //                 zipFileName         = "sds-dfp-config1"
        //                 outputPathPrefix    = "codebuild-dfp-workbench"
        //             } else if ("${ModuleName}" == 'Airflow-v1'){
        //                 zipFileName         = "sds-config-airflow1"
        //                 outputPathPrefix    = "codebuild-orchestration"
        //             }
        //         }
        //     }
        // }

        // stage ('getTheBuildFromS3') {
        //     steps{
        //         script {
        //             dir("${projectName}/${deploy_environment}/${buildS3SourcePath}") {
        //                 buildPath = "${deploy_environment}/" + "${buildS3SourcePath}" + "${BUILD_VERSION}"
        //                 deploy.getBuildFromArtifactory(buildPath: "${buildPath}")
        //             }
        //         }
        //     }
        // }

        // stage ('createDeployableZip') {
        //     steps{
        //         script {
        //             dir("${projectName}/${deploy_environment}/${buildS3SourcePath}/") {
        //                 BuildName = sh(returnStdout: true, script: "find . -name *.zip |awk -F '/' '{print \$2}'")
        //                 if ("${ModuleName}" == 'Airflow'){
        //                     deploy.createDeployaleFileOnCondition(deployFileName:"${zipFileName}",moduleName:"${ModuleName}")
        //                 } else if ("${ModuleName}" == 'AnalyticalJobs'){
        //                     sh "mkdir -p config/latest/sds_spark_config/"
        //                     sh "unzip -o ${BuildName}"
        //                     sh "cp sds_spark_configs/qa/* config/latest/sds_spark_config/"
        //                     sh "find * -maxdepth 0 -type d -not -iname config -exec rm -rf {} \\;"
        //                     sh "rm -f ${BuildName}"
        //                     sh "rm -f branch.version"
        //                     sh "rm -rf .git"
        //                     sh "rm -rf .gitignore"
        //                     deploy.createDeployaleFileOnCondition(deployFileName:"${zipFileName}",moduleName:"No-Module")
        //                 } else if ("${ModuleName}" == 'Airflow-v1'){
        //                     deploy.createDeployaleFileOnCondition(deployFileName:"${zipFileName}",moduleName:"${ModuleName}")
        //                 }
        //             }
        //         }
        //     }
        // }

        // stage ('deployingTheBuild') {
        //     steps{
        //         script {
        //             dir("${projectName}/${deploy_environment}/${buildS3SourcePath}/"){
        //                 deployPath = "${destinationPath}" + "${outputPathPrefix}/"
        //                 deploy.deployment(deployPath:"${deployPath}", deployFileName:"${zipFileName}")
        //             }
        //         }
        //     }
        // }

    }

    // publishHTML ([allowMissing: false,
    //                 alwaysLinkToLastBuild: false,
    //                 keepAll: true,
    //                 reportDir: '',
    //                 reportFiles: 'myreport.html',
    //                 reportName: 'My Reports',
    //                 reportTitles: 'The Report'])
}
