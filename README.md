# NAME

Voson::Plugin::Dispatch - Dispatcher Plugin for Voson

# DESCRIPTION

This plugin provides dispatcher feature to Voson.

# SYNOPSIS

    use Voson plugins => ['Dispatch'];
    

    my $users = {};
    

    app {
        get '/' => sub { [200, [], 'Hello, World!'] };
        get '/user/:id' => sub {
            my $id = path_param('id');
            my $user = $users->{$id};
            $user ? 
                [200, [], sprintf('name = %s', $user->{name}) ]
                [404, [], 'no such user']
            ;
        };
        post '/user/:id' => sub {
            my $id = path_param('id');
            my $name = param('name'); 
            $users->{$id} = { name => $name };
            [200, [], 'registered!'];
        };
    };

# DSL

## get post put del

    get $path => sub { ... };

Add action for $path. You may use [Router::Simple](http://search.cpan.org/perldoc?Router::Simple) syntax in $path.

## path\_param

    get '/user/:id' => sub {
        my $id = path_param('id');
        ### or 
        my $path_params = path_param;
        $id = $path_params->{id};
        ...
    };

Fetch captured parameter from PATH\_INFO.

# LICENSE

Copyright (C) ytnobody.

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# AUTHOR

ytnobody <ytnobody@gmail.com>
