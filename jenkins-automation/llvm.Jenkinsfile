#!groovy

pipeline{

    agent any
    options {
        skipDefaultCheckout()
    }
    parameters{
        string(name: "TOOLCHAIN_PATH", defaultValue: "/home/johnathan/jenkins-automation/toolchain", trim: false, description: "Cross-compiler toolchain path")
        //string(name: "SYSROOT_PATH", defaultValue: "/home/johnathan/jenkins-automation/sysroot", trim: false, description: "Linux system root path")
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
                git url: 'https://github.com/llvm/llvm-project.git', branch: 'release/18.x'
            }
        }
        stage('Build LLVM'){
            steps {
                sh script: "mkdir -p ${params.TOOLCHAIN_PATH}"
                sh script: $/mkdir -p build; cd build; cmake -G "Ninja" -DCMAKE_BUILD_TYPE=Release -DLLVM_INCLUDE_EXAMPLES=Off -DCMAKE_INSTALL_PREFIX=${params.TOOLCHAIN_PATH} -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ -DLLVM_LINK_LLVM_DYLIB=ON -DLLVM_ENABLE_PROJECTS="clang;lld" ../llvm/$, label: 'configure LLVM'
                sh script: "cd build && cmake --build . --target install", label: 'build LLVM'

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
