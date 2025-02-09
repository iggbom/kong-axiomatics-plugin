# Kong Axiomatics

A plugin that integrates Kong with an Axiomatics PDP endpoint.

## Description

Before proxying the request to an API upstream of Kong, this plugin will send a XACML JSON POST request to an Axiomatics PDP endpoint and based on the response determine whether to proceed or return.

## Installation

### With a local instance of Kong

Clone this repo

<pre>
$ git clone https://github.com/iggbom/kong-axiomatics-plugin
$ cd kong-axiomatics-plugin
$ luarocks make *.rockspec
</pre>

You will also have to add the kong-axiomatics-plugin in your configuration file.
If you are starting from the default kong.conf file uncomment the plugins key and add this one

<pre>
  plugins = bundled, kong-axiomatics-plugin
</pre>

Restart Kong using this configuration file and you're ready to go

<pre>
  kong stop
  kong start -c /etc/kong/kong.conf
</pre>

### With docker

Start Kong

<pre>
  docker-compose up -d
</pre>

Check the log and make sure that Kong has started
<pre>
  docker-compose logs -f kong
</pre>

Add the Axiomatics plug-in
<pre>
  ./addCustomPlugin.sh
</pre>

Create a sample service
<pre>
  ./createExampleService.sh
</pre>

Stop Kong as well as remove Docker volume to be able to start from scratch

<pre>
  docker-compose down -v
</pre>

## Configuration

<table>
  <thead>
    <tr>
      <th>Form Parameter</th>
      <th>Required</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>config.pdp_url</code></td>
      <td>yes</td>
      <td></td>
      <td>The URL to which the plugin will make a JSON <code>POST</code> request before proxying the original request.</td>
    </tr>
    <tr>
      <td><code>config.token_header_name</code></td>
      <td>yes</td>
      <td>Authorization</td>
      <td>The name of the header that carries the JWT</td>
    </tr>
    <tr>
      <td><code>config.claims_to_include</code></td>
      <td>no</td>
      <td></td>
      <td>A list of strings that correspond to the claims we are interested in forwarding to the PDP from the JWT</td>
    </tr>
    <tr>
      <td><code>config.pdp_username</code></td>
      <td>yes</td>
      <td></td>
      <td>The user that is allowed to send a request to the PDP</td>
    </tr>
    <tr>
      <td><code>config.pdp_password</code></td>
      <td>yes</td>
      <td></td>
      <td>The password for the PDP user</td>
    </tr>
    <tr>
      <td><code>config.url_parameter_matching</code></td>
      <td>no</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td><code>config.url_parameter_key</code></td>
      <td>no</td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>

## Author
Initial author: Ioannis Iordanidis </br>
Continued work by: Jonas Iggbom

## License
<pre>
  The MIT License (MIT)
  =====================

  Copyright (c) 2019 Ioannis P. Iordanidis

  The software is provided "as is", without warranty of any kind, express or
  implied, including but not limited to the warranties of merchantability,
  fitness for a particular purpose and noninfringement. In no event shall the
  authors or copyright holders be liable for any claim, damages or other
  liability, whether in an action of contract, tort or otherwise, arising from,
  out of or in connection with the software or the use or other dealings in
  the software.
</pre>
