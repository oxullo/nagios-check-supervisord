# nagios-check-supervisord
Nagios/Icinga plugin for supervisord via XMLRPC

## Supervisord Configuration

    [inet_http_server]
    port = :9001
    username = user
    password = password

## Nagios Configuration

Command declaration:

    define command {
            command_name                    check_supervisord
            command_line                    $USER1$/check_supervisord -H $HOSTNAME$ -n $ARG1$
    }
    
    define command {
            command_name                    check_supervisord_auth
            command_line                    $USER1$/check_supervisord -H $HOSTNAME$ -n $ARG1$ -u '$ARG2$' -p '$ARG3$'
    }


Simplest service declaration:

    define service {
        use                             generic-service
        host_name                       hostname
        service_description             supervisord service
        check_command                   check_supervisord!processname
    }

With authentication:

    define service {
        use                             generic-service
        host_name                       hostname
        service_description             supervisord service
        check_command                   check_supervisord_auth!processname!user!password
    }

## Kudos

Thanks to [timgws][1].

[1]: https://github.com/timgws/nagios-supervisord-processes
