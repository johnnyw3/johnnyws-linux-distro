#!groovy

pipeline{

    agent any
    options {
        skipDefaultCheckout()
    }
    parameters{
        //string(name: "TOOLCHAIN_PATH", defaultValue: "/home/johnathan/jenkins-automation/toolchain", trim: false, description: "Cross-compiler toolchain path")
        string(name: "SYSROOT_PATH", defaultValue: "/home/johnathan/jenkins-automation/sysroot", trim: false, description: "Linux system root path")
    }
    stages{
        /*
         * stage('Setup workspace'){
         *    steps {
         *        sh script: 'echo test'
         *    }
         * }
         */
        stage('Checkout SCM'){
            steps{
                sh script: "ls ${params.SYSROOT_PATH}", label: "assert SYSROOT_PATH parameter is valid"
                git url: 'https://sourceware.org/git/glibc.git', branch: 'release/2.39/master'
            }
        }
        stage('Build glibc'){
            steps {
                sh script: 'mkdir -p build'
                dir('build'){
                    // LLVM cannot build glibc
                    sh script: $/../configure BUILD_CC=gcc CC=gcc CXX=g++ --target=x86_64-linux --build=x86_64-pc-linux-gnu --host=x86_64-pc-linux-gnu \
                                 --with-sysroot=${params.SYSROOT_PATH} --with-headers=${params.SYSROOT_PATH}/usr/include --prefix=/usr \
                                 --enable-kernel=6.6.0 libc_cv_slibdir=/usr/lib/$, label: 'configure glibc'
                    sh script: 'make -j16', label: 'build glibc'
                    sh script: "make DESTDIR=${params.SYSROOT_PATH} install -j16", label: 'install glibc'
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
