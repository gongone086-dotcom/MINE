name: Minecraft Server (Temporary)

on:
  workflow_dispatch:  # تقدر تشغله يدوي من تبويب Actions

jobs:
  run-server:
    runs-on: ubuntu-latest
    timeout-minutes: 360  # أقصى مدة 6 ساعات
    steps:
      - name: Download PaperMC server jar
        run: |
          mkdir server
          cd server
          wget -O paper.jar https://api.papermc.io/v2/projects/paper/versions/1.20.1/builds/123/downloads/paper-1.20.1-123.jar
          echo "eula=true" > eula.txt

      - name: Start Minecraft Server
        run: |
          cd server
          nohup java -Xmx2G -Xms1G -jar paper.jar nogui &
          echo "Minecraft server started!"
          sleep 21000  # يفضل ما بين 5-6 ساعات تشغيل
