# Configure Private Google Access in Firestore with MongoDB compatibility

This page describes how to enable and configure Private Google Access in Firestore with MongoDB compatibility.

## About Private Google Access in Firestore with MongoDB compatibility

By default, when a Compute Engine VM lacks an external IP address assigned to its network interface, it can only send packets to other internal IP address destinations. You can allow these VMs to connect to the Firestore with MongoDB compatibility service by enabling Private Google Access on the subnet used by the VM's network interface.

### Applicable services and protocols

  - Instructions in this guide **apply only to Firestore with MongoDB compatibility** .

  - The default and VIP domains used by the Firestore with MongoDB compatibility and their IP ranges support only the MongoDB protocol on port 443. All other protocols aren't supported.

**Note:** To configure Private Google Access for Firestore and other services, see [Configure Private Google Access](https://cloud.google.com/vpc/docs/configure-private-google-access) .

### Network requirements

A VM interface can reach Google APIs and services through the internal Google network using Private Google Access if all these conditions are met:

  - The VM interface is connected to a subnet where Private Google Access is enabled.

  - The VM interface doesn't have an external IP address assigned.

  - The source IP address of packets sent from the VM matches one of the following IP addresses.
    
      - The VM interface's primary internal IPv4 address
      - An internal IPv4 address from an alias IP range

A VM with an [external IPv4 address assigned to its network interface](https://cloud.google.com/vpc/docs/ip-addresses) doesn't need Private Google Access to connect to Google APIs and services. However, the VPC network must meet [the requirements for accessing Google APIs and services](/vpc/docs/access-apis-external-ip#requirements) .

### IAM permissions

Project owners, editors, and IAM principals with the [Network Admin](https://cloud.google.com/compute/docs/access/iam#compute.networkAdmin) role can create or update subnets and assign IP addresses.

For more information on roles, read the [IAM roles](https://cloud.google.com/compute/docs/access/iam) documentation.

### Logging

Cloud Logging captures all API requests made from VM instances in subnets that have Private Google Access enabled. Log entries identify the source of the API request as an internal IP address of the calling instance.

You can configure daily usage and monthly rollup reports to be delivered to a Cloud Storage bucket. See the [Viewing Usage Reports](https://cloud.google.com/compute/docs/usage-export) page for details.

## Configuration summary

The following table summarizes the different ways that you can configure Private Google Access in Firestore with MongoDB compatibility. For more detailed instructions information, see [Network configuration](#network-configuration) .

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Domain option</th>
<th>IP ranges</th>
<th>DNS configuration</th>
<th>Routing configuration</th>
<th>Firewall configuration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Default domain ( <code dir="ltr" translate="no">        firestore.goog       </code> )</p>
<p>The default domains are used when you don't configure DNS records for <code dir="ltr" translate="no">        restricted.firestore.goog       </code> .</p></td>
<td><code dir="ltr" translate="no">       136.124.0.0/23      </code></td>
<td>You access the Firestore with MongoDB compatibility service through its public IP addresses, so no special DNS configuration is required.</td>
<td><p>Check that your VPC network can route traffic to the IP address ranges that are used by the Firestore with MongoDB compatibility service.</p>
<ul>
<li><a href="#config-routing-default">Basic configuration</a> : Confirm that you have default routes with next hop <code dir="ltr" translate="no">         default-internet-gateway        </code> and a destination range of <code dir="ltr" translate="no">         0.0.0.0/0        </code> . Create those routes if they are missing.</li>
<li><a href="#config-routing-custom">Custom configuration</a> : Create routes to the <code dir="ltr" translate="no">         136.124.0.0/23        </code> IP address range.</li>
</ul></td>
<td><p>Check that your <a href="#config-firewall">firewall rules</a> allow egress to the <code dir="ltr" translate="no">        136.124.0.0/23       </code> IP address range.</p>
<p>The default allow egress firewall rule allows this traffic, if there is no higher priority rule that blocks it.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        restricted.firestore.goog       </code></p>
<p>Use <code dir="ltr" translate="no">        restricted.firestore.goog       </code> to access the Firestore with MongoDB compatibility service by using a set of IP addresses only routable from within Google Cloud. Can be used in VPC Service Controls scenarios.</p></td>
<td><code dir="ltr" translate="no">       199.36.153.2/31      </code></td>
<td>Configure <a href="#config-domain">DNS records</a> to send requests to the <code dir="ltr" translate="no">       199.36.153.2/31      </code> IP address range.</td>
<td>Check that your VPC network has <a href="#config-routing-custom">routes</a> to the <code dir="ltr" translate="no">       199.36.153.2/31      </code> IP address range.</td>
<td>Check that your <a href="#config-firewall">firewall rules</a> allow egress to the <code dir="ltr" translate="no">       199.36.153.2/31      </code> IP address range.</td>
</tr>
</tbody>
</table>

## Network configuration

This section describes how to configure your network to access the Firestore with MongoDB compatibility using Private Google Access.

### DNS configuration

**Note:** There are public DNS records `  restricted.firestore.goog  ` . However, you can't use the public records when you configure Private Google Access. You must create a private DNS zone and records.

Unlike other Google APIs, the Firestore with MongoDB compatibility API uses different domain names and IP addresses for Private Google Access:

  - `  restricted.firestore.goog  ` enables API access to the Firestore with MongoDB compatibility API.
    
      - IP addresses: `  199.36.153.2  ` and `  199.36.153.3  ` .
    
      - Because Firestore with MongoDB compatibility is compliant with VPC Service Controls, you can use this domain in VPC Service Controls scenarios.

To create a DNS zone and records for Firestore with MongoDB compatibility:

1.  Create a private DNS zone for `  firestore.goog  ` .
    
    Consider [creating a Cloud DNS private zone](https://cloud.google.com/dns/zones#create-private-zone) for this purpose.

2.  In the `  firestore.goog  ` zone, create the following records:
    
    1.  An `  A  ` record for `  restricted.firestore.goog  ` that points to the following IP addresses: `  199.36.153.2  ` and `  199.36.153.3  ` .
    
    2.  A `  CNAME  ` record for `  *.firestore.goog  ` that points to `  restricted.firestore.goog  ` .
    
    To create these records in Cloud DNS, see [add a record](https://cloud.google.com/dns/docs/records#add_a_record) .

### Routing configuration

Your VPC network must have appropriate routes whose next hops are the default internet gateway. Google Cloud doesn't support routing traffic to Google APIs and services through other VM instances or custom next hops. Despite being called *default internet gateway* , packets sent from VMs in your VPC network to Google APIs and services remain within Google's network.

  - If you select the default domain option, your VM instances connect to the Firestore with MongoDB compatibility service using the following public IP address range: `  136.124.0.0/23  ` . These IP addresses are publicly routable, but the path from a VM in a VPC network to those addresses remains within Google's network.

  - Google doesn't publish routes on the internet to any of the IP addresses used by the `  restricted.firestore.goog  ` domain. Consequently, this domain can only be accessed by VMs in a VPC network or on-premises systems connected to a VPC network.

If your VPC network contains a [default route](https://cloud.google.com/vpc/docs/vpc#routingpacketsinternet) whose next hop is the default internet gateway, you can use that route to access the Firestore with MongoDB compatibility service, without needing to create custom routes. See [routing with a default route](#config-routing-default) for details.

If you have replaced a default route (destination `  0.0.0.0/0  ` or `  ::0/0  ` ) with a custom route whose next hop is *not* the default internet gateway, you can meet the routing requirements for the Firestore with MongoDB compatibility service [using custom routing](#config-routing-custom) instead.

#### Routing with a default route

Each VPC network contains an IPv4 default route ( `  0.0.0.0/0  ` ) when it is created.

The default route provides a path to the IP addresses for the following destinations:

  - Default domain ( `  firestore.goog  ` ): `  136.124.0.0/23  `
  - `  restricted.firestore.goog  ` : `  199.36.153.2/31  `

For Google Cloud console and Google Cloud CLI instructions on how to check the configuration of a default route in a given network, see [Configure Private Google Access](https://cloud.google.com/vpc/docs/configure-private-google-access#config-routing-default) .

#### Routing with custom routes

As an alternative to a default route, you can use custom static routes, each having a more specific destination, and each using the default internet gateway next hop. The destination IP addresses for the routes depend on [the domain that you choose](#summary) :

  - Default domain ( `  firestore.goog  ` ): `  136.124.0.0/23  `
  - `  restricted.firestore.goog  ` : `  199.36.153.2/31  `

For Google Cloud console and Google Cloud CLI instructions on how to check the configuration of custom routes in a given network, see [Configure Private Google Access](https://cloud.google.com/vpc/docs/configure-private-google-access#config-routing-custom) .

### Firewall configuration

The firewall configuration of your VPC network must allow access from VMs to the IP addresses used by the Firestore with MongoDB compatibility service. The implied `  allow egress  ` rule satisfies this requirement.

In some firewall configurations, you need to create specific egress allow rules. For example, suppose you've created an egress deny rule that blocks traffic to all destinations ( `  0.0.0.0  ` for IPv4). In that case, you must create one egress allow firewall rule whose priority is higher than the egress deny rule for each IP address range used by the [the domain that you choose](#summary) :

  - Default domain ( `  firestore.goog  ` : `  136.124.0.0/23  `
  - `  restricted.firestore.goog  ` : `  199.36.153.2/31  `

To create firewall rules, see [Creating firewall rules](https://cloud.google.com/vpc/docs/using-firewalls#creating_firewall_rules) . You can limit the VMs to which the firewall rules apply when you define [the target](https://cloud.google.com/vpc/docs/firewalls#rule_assignment) of each egress allow rule.

## Private Google Access configuration

You can enable Private Google Access after you've met the [network requirements](#network-requirements) in your VPC network. For Google Cloud console and Google Cloud CLI instructions, follow the steps outlined in [Enable Private Google Access](https://cloud.google.com/vpc/docs/configure-private-google-access#enabling-pga) .

## What's next

  - [Securing with VPC Service Controls](/firestore/mongodb-compatibility/docs/securing-with-vpc-sc)
  - [Configure Private Google Access](https://cloud.google.com/vpc/docs/configure-private-google-access)
