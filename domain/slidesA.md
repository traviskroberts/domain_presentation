!SLIDE transition=toss

# Custom Domains - routes.rb #

	@@@ ruby
	MyApp::Application.routes.draw do

	  constraints(Domain)do
	    match '/' => 'site#domain', :as => 'domain'
	  end

	  root :to => 'site#index'

	end

!SLIDE transition=toss

# /lib/domain.rb #

	@@@ ruby
	class Domain
	  def self.matches?(request)
	    request.domain.present? && request.domain != "lvh.me"
	  end
	end

!SLIDE transition=toss

# httpd.conf #

	<VirtualHost *:80>
	  ServerName mysite.com
	  ServerAlias www.mysite.com

	  DocumentRoot "/path/to/project"

	  <Directory "/path/to/project">
	    Options FollowSymLinks MultiViews Includes
	    AllowOverride All
	    Order allow,deny
	    Allow from all
	  </Directory>
	</VirtualHost>

!SLIDE transition=fade

# httpd.conf #

	<VirtualHost *:80>
	  DocumentRoot "/path/to/project"

	  <Directory "/path/to/project">
	    Options FollowSymLinks MultiViews Includes
	    AllowOverride All
	    Order allow,deny
	    Allow from all
	  </Directory>
	</VirtualHost>

!SLIDE transition=toss

# Examples! #