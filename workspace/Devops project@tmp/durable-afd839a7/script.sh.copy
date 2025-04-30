
                            # Create a clean temporary directory
                            TEMP_DIR=$(mktemp -d)
                            
                            # Clone the repository into temp directory
                            git clone https://github.com/pulkitraj9897/pulkit9897.github.io.git $TEMP_DIR
                            
                            # Copy your local files to the cloned repository
                            cp -r /var/local/flask-site/* $TEMP_DIR/
                            
                            # Configure git
                            cd $TEMP_DIR
                            git config user.email "pulkitraj9897@gmail.com"
                            git config user.name "pulkit9897"
                            
                            # Commit and push changes using the token
                            git add .
                            git commit -m "Automated commit 1" || echo "No changes to commit"
                            git push https://${GITHUB_TOKEN}@github.com/pulkitraj9897/pulkit9897.github.io.git main
                            
                            # Clean up
                            cd ..
                            rm -rf $TEMP_DIR
                        