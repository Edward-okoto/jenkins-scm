# jenkins-scm

job('My-Freestyle-Job') {
    description('A sample Jenkins freestyle project that clones a GitHub repository, builds the project, and archives artifacts.')

    // Source Code Management: Git
    scm {
        git {
            remote {
                url('https://github.com/yourusername/yourrepository.git')
            }
            branch('*/main')
        }
    }
    
    // Optionally, poll the repository every 5 minutes for changes
    triggers {
        scm('H/5 * * * *')
    }
    
    // Build Steps: Execute Shell command
    steps {
        shell('''#!/bin/bash
echo "Starting the build process..."
# Example: Run your build script or any commands
./build.sh
echo "Build process completed!"
''')
    }
    
    // Post-build actions: Archive build artifacts (adjust the pattern as needed)
    publishers {
        archiveArtifacts('**/build/*.jar, **/build/*.war')
    }
}
