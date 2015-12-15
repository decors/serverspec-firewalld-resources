# Serverspec Firewalld resources
Serverspec resources to testing Firewalld.

## Resources

### firewalld

#### usage

* default zone

        describe firewalld do
          its(:default_zone) { should contain 'public' }
        end
    
* port

        describe firewalld do
          it { should have_port('161/udp') }
        end

* service

        describe firewalld do
          it { should have_service('ssh') }
        end

* interface

        describe firewalld do
          it { should have_interface('eth0') }
        end

* rich rule

    * text

            describe firewalld do
              it { should have_rich_rule('rule family="ipv4" source address="1.1.1.100/32" service name="mysql" accept') }
            end

    * hash

        * source / destination and service example

                describe firewalld do
                  it do 
                    should have_rich_rule(
                      :family => 'ipv4',
                      :source => '1.1.1.100/32',
                      :service => 'mysql',
                      :action  => 'accept'
                    )
                  end
                end

        * port and protocol example

                describe firewalld do
                  it do
                    should have_rich_rule(
                      :family => 'ipv4',
                      :port => { :port => '80', :protocol => 'tcp' },
                      :action  => 'accept'
                    )
                  end
                end

        * service and logging example

                describe firewalld do
                  it do
                    should have_rich_rule(
                      :family => 'ipv4',
                      :service => 'ssh',
                      :log => { :prefix => 'ssh con', :level => 'info' },
                      :action  => 'accept'
                    )
                  end
                end

* (option) zone

        describe firewalld do
          it { should have_port('161/udp').with_zone('public') }
        end

* (option) permanently

        describe firewalld do
          it { should have_port('161/udp').with_permanent }
        end