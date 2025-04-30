
                        rm -rf site
                        git clone https://github.com/pulkitraj9897/pulkit9897.github.io.git site
                        cd site
                        cp -r ../* ../.* . 2>/dev/null || true
                        git config user.email "pulkitraj9897@gmail.com"
                        git config user.name "pulkit9897"
                        git add .
                        git commit -m "Automated commit ${BUILD_NUMBER}" || echo "No changes to commit"
                        git push https://${GITHUB_TOKEN}@github.com/pulkitraj9897/pulkit9897.github.io.git main
                    