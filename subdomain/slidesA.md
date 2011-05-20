!SLIDE transition=toss

# Subdomains - routes.rb #

	@@@ ruby
	MyApp::Application.routes.draw do

	  constraints(Subdomain)do
	    match '/' => 'site#subdomain', :as => 'subdomain'
	  end

	  root :to => 'site#index'

	end

!SLIDE transition=toss

# /lib/subdomain.rb #

	@@@ ruby
	class Subdomain
	  def self.matches?(request)
	    request.subdomain.present? && request.subdomain != 'www'
	  end
	end

!SLIDE transition=toss

# app/helpers/url_helper.rb #

	@@@ ruby
	module UrlHelper
	  def with_subdomain(subdomain)
	    subdomain = (subdomain || "")
	    subdomain += "." unless subdomain.empty?
	    [subdomain, request.domain, request.port_string].join
	  end

	  def url_for(options = nil)
	    if options.kind_of?(Hash) && options.has_key?(:subdomain)
	      options[:host] = with_subdomain(options.delete(:subdomain))
	    end
	    super
	  end
	end

!SLIDE transition=toss

# Include the helper #

	@@@ ruby
	class ApplicationController < ActionController::Base
	
	  include UrlHelper
	
	end

!SLIDE transition=toss

# Link to subdomains #

	@@@ ruby
	link_to "Subdomain Page", subdomain_url(:subdomain => 'test')
	
	link_to "Home Page", root_url(:subdomain => false)
