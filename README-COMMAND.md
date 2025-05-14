##START HAZELCAST
#create config and data folder
docker-compose up -d and docker-compose down
#change permission all folder
chmod -R 755 mc-data,hazelcast-data,config
#start containers again
docker-compose up -d
##FIX ERROR STOP SUDDENLY
#remove or delete old mc.lock file because it store old status value of hzcast management center instance
sudo rm ./mc-data/mc.lock
#ORDER STOP
#stop hazelcast man center first
docker stop [container-id-management-center]
#stop hazelcast nodes
docker stop [container-id-hazelcast]
##Check Before Restarting
#Before restarting the stack, if you suspect the previous shutdown wasn't proper:
#Check that no containers are still running:
docker ps | grep -E "hazelcast|management-center"
#Check for and remove lock files if needed:
ls -la ./mc-data/mc.lock  # Check if lock file exists
rm ./mc-data/mc.lock      # Remove lock file if it exists
#Following this proper shutdown procedure will help prevent issues like lingering lock files and startup problems in the future.
