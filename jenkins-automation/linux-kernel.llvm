#!groovy

pipeline{

    agent any
    options {
        skipDefaultCheckout()
    }
    //parameters{
        //string(name: "TOOLCHAIN_PATH", defaultValue: "/home/johnathan/jenkins-automation/toolchain", trim: false, description: "Cross-compiler toolchain path")
        //string(name: "SYSROOT_PATH", defaultValue: "/home/johnathan/jenkins-automation/sysroot", trim: false, description: "Linux system root path")
    //}
    stages{
        /*
         * stage('Setup workspace'){
         *    steps {
         *        sh script: 'echo test'
         *    }
         * }
         */
        stage('Download kernel sources'){
            steps{
                sh script: 'wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.6.16.tar.xz', label: 'download source tarball'
                sh script: 'tar -xvf linux-6.6.16.tar.xz', label: 'untar downloaded tarball'
                sh script: 'rm linux-6.6.16.tar.xz*', label: 'deleted downloaded tarball'
                sh script: 'cd linux-6.6.16; makr mrproper', label: 'clean linux directory'
            }
        }
        stage('Build Linux-Headers'){
            steps {
                dir('linux-6.6.16'){
                    // Using host toolchain for now, but this is okay since it is just the headers
                    sh script: 'make headers', label: 'build linux-headers'
                    sh script: 'tar -czvf linux-headers-6.6.16.tar.gz usr/include/**/*.h', label: 'create header tarball'
                    archiveArtifacts artifacts: 'linux-headers-6.6.16.tar.gz', followSymlinks: false, fingerprint: true
                }
            }
        }
    }
    /*post{
     *   always{
     *       junit 'results.xml'
     *   }
     * }
     */
}
