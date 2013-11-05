# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

#
# Configuration for the WordPress
#

WP_VERSION           = 'latest' # latest or 3.4 or later or http(s):// URL to zipfile
WP_LANG              = "en" # WordPress locale (e.g. ja)

WP_HOSTNAME          = "wordpress.test" # e.g example.com
WP_IP                = "33.33.33.10" # host ip address

WP_TITLE             = "Welcome to the site" # title
WP_ADMIN_USER        = "admin" # default user
WP_ADMIN_PASS        = "admin" # default user's password

WP_DB_PREFIX         = 'wp_' # Database prefix

WP_DEFAULT_PLUGINS   = %w(theme-check plugin-check hotfix) # default plugins
WP_DEFAULT_THEME     = '' # e.g. twentythirteen

WP_DIR               = '' # e.g. /wp or wp or other
WP_IS_MULTISITE      = false # enable multisite when true
WP_FORCE_SSL_ADMIN   = false # enable force ssl admin when true
WP_DEBUG             = true # enable debug mode
WP_SAVEQUERIES       = false # save the database queries to an array
WP_THEME_UNIT_TEST   = false # automatic import theme unit test data

WP_ALWAYS_RESET      = false # always reset database

WP_CHEF_COOKBOOKS_PATH = Dir.pwd # path to the cookbooks (e.g. ~/vagrant-local)

# end configuration




Vagrant.configure("2") do |config|
  config.vm.hostname = WP_HOSTNAME
  #config.vm.network :private_network, ip: WP_IP

  #config.vm.synced_folder "www/", "/var/www", :create => "true"

  config.hostsupdater.remove_on_suspend = true

  config.vm.box = "saturizedtest"

  #config.vm.box_url = "debian-7.1.box"
  config.vm.box_url = "https://dl.dropboxusercontent.com/u/228224/wheezy32.box"

  config.vm.network :private_network, ip: "33.33.33.10"
  # Here's a folder for passing stuff back and forth
  config.vm.synced_folder "./shared", "/home/vagrant/host_shared"

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbook"]
    chef.add_recipe "apt"
    chef.add_recipe "build-essential"
    chef.add_recipe "mysql::server"
    chef.add_recipe "nginx"
    chef.add_recipe "postfix"
    chef.add_recipe "php"
    chef.add_recipe "php::module_apc"
    chef.add_recipe "php::module_curl"
    chef.add_recipe "php::module_gd"
    chef.add_recipe "php::module_mysql"   
    chef.add_recipe "php-fpm"
    chef.add_recipe "wp-cli"
    chef.add_recipe "wp-install"
    chef.json = {
      "mysql" => { 
        "dbhost" => "localhost",
        "database" => "wordpressdb",
        "dbuser" => "wordpressuser",
        "server_root_password"  => "password",
        "bind_address"      => "127.0.0.1",
        "allow_remote_root"   => true
      },
      :"wp-install" => {
        :wp_version        => WP_VERSION,
        :url               => "http://" << File.join(WP_HOSTNAME, WP_DIR),
        :wpdir             => File.join('/var/www', WP_DIR),
        :locale            => WP_LANG,
        :admin_user        => WP_ADMIN_USER,
        :admin_password    => WP_ADMIN_PASS,
        :dbprefix          => WP_DB_PREFIX,
        :default_plugins   => WP_DEFAULT_PLUGINS,
        :default_theme     => WP_DEFAULT_THEME,
        :title             => WP_TITLE,
        :is_multisite      => WP_IS_MULTISITE,
        :force_ssl_admin   => WP_FORCE_SSL_ADMIN,
        :debug_mode        => WP_DEBUG,
        :savequeries       => WP_SAVEQUERIES,
        :theme_unit_test   => WP_THEME_UNIT_TEST,
        :always_reset      => WP_ALWAYS_RESET,
        :dbhost            => "localhost"
      
      }
      }
  end
end