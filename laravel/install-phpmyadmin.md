# Install ```phpmyadmin``` on your Laravel Homestead box #

### NOTE: Before destroying the Vagrant box, **and losing all our database entries**, you should backup the database ###

1. ```$ vagrant ssh``` into your vagrant box

2. ```$ cd laravel```

3. Run ```$ mysqldump portal > portal.sql``` - This will create a SQL file so that we can re-import once phpmyadmin is running

### Make sure the portal.sql file is not empty (```cat``` it) then ```$ exit``` out of your Vagrant box and proceed... (you should be in the ```~/Homestead``` folder) ###

1. ```$ vagrant destroy```

2. In your ```~/Projects``` folder create a new folder (use ```mkdir``` or Finder/File Manager) named ```phpmyadmin```

3. Back in the ```$ ~/Homestead``` folder edit the ```Homestead.yaml``` file to include "folder" and "site" mapping (phpmyadmin.local) to the ```phpmyadmin``` folder you just created

4. ```$ vagrant up```

5. ```$ vagrant ssh```

6. Run ```$ composer create-project phpmyadmin/phpmyadmin``` in your ```vagrant``` folder - DO NOT run this from within your ```phpmyadmin``` folder!

7. ```$ composer update```

8. Edit your "hosts" file (mac: ```$ sudo nano /etc/hosts```) to add an entry for ```phpmyadmin.local``` that points to your Vagrant box's IP address of  ```192.168.10.10``` (if one already exists do not add one)

9. In your browser try visiting  ```phpmyadmin.local```  (username is 'root' and password is 'secret')

### Now that phpmyadmin is running, we'll need to fix a thing in the sql file and then import it ###

1. ssh Into your vagrant box

2. cd Into the laravel folder

3. nano The ```portal.sql``` file

4. Add ```USE portal;```

5. Exit and save

6. Run ```$ mysql < portal.sql```

And you are done!
