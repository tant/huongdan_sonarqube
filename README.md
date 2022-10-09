# huongdan_sonarqube


Theo hướng dẫn chính chủ của SonarQube:
Because SonarQube uses an embedded Elasticsearch, make sure that your Docker host configuration complies with the Elasticsearch production mode requirements and File Descriptors configuration.

For example, on Linux, you can set the recommended values for the current session by running the following commands as root on the host:
sysctl -w vm.max_map_count=524288
sysctl -w fs.file-max=131072
ulimit -n 131072
ulimit -u 8192

Nhớ là server này chạy linux cho nên nếu máy của mình đang là windows thì mình phải vô wsl để chỉnh mới ăn thua
wsl -d docker-desktop
sysctl -w vm.max_map_count=262144


Lệnh docker chỉ
docker run \
    --rm \
    -e SONAR_HOST_URL="http://[thay bằng ip]:[thay bằng port]" \
    -e SONAR_LOGIN="[thay bằng token của mình]" \
    -v "${YOUR_REPO}:/usr/src" \
    sonarsource/sonar-scanner-cli

Lệnh sonarqube gợi ý lúc tạo project:
sonar-scanner.bat -D"sonar.projectKey=test" -D"sonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.login="[thay bằng token của project]"
Lệnh anh đã chạy
docker run --rm  --network=sonarqube_default -e SONAR_HOST_URL="http://[thay bằng ip:9000" -e SONAR_LOGIN="[thay bằng token của project]"  -v "%cd%:/usr/src" sonarsource/sonar-scanner-cli
