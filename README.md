# NAME

Otogiri - A lightweight medicine for using database

# SYNOPSIS

    use Otogiri;
    my $db = Otogiri->new(connect_info => ['dbi:SQLite:...', '', '']);
    

    $db->insert(book => {title => 'mybook1', author => 'me', ...});

    my $book_id = $db->last_insert_id;
    my $row = $db->single(book => {id => $book_id});

    print 'Title: '. $row->{title}. "\n";
    

    my @rows = $db->select(book => {price => {'>=' => 500}});
    for my $r (@rows) {
        printf "Title: %s \nPrice: %s yen\n", $r->{title}, $r->{price};
    }
    

    $db->update(book => [author => 'oreore'], {author => 'me'});
    

    $db->delete(book => {author => 'me'});
    

    ### using transaction
    do {
        my $txn = $db->txn_scope;
        $db->insert(book => ...);
        $db->insert(store => ...);
        $txn->commit;
    };

# DESCRIPTION

Otogiri is a thing that like as ORM. A slogan is "Schema-less, Fat-less".

# ATTRIBUTES

Please see ATTRIBUTES section of [DBIx::Otogiri](http://search.cpan.org/perldoc?DBIx::Otogiri) documentation.

# METHODS

## new

    my $db = Otogiri->new( connect_info => [$dsn, $dbuser, $dbpass] );

Instantiate and connect to db. Then, it returns [DBIx::Otogiri](http://search.cpan.org/perldoc?DBIx::Otogiri) object.

Please see ATTRIBUTE section.

# INFORMATION ABOUT INCOMPATIBILITY

## version 0.11

- An insert() method is removed, and it was become a synonym of fast\_insert() method.

# LICENSE

Copyright (C) ytnobody.

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# AUTHOR

ytnobody <ytnobody@gmail.com>

# SEE ALSO

[DBIx::Otogiri](http://search.cpan.org/perldoc?DBIx::Otogiri)

[DBIx::Sunny](http://search.cpan.org/perldoc?DBIx::Sunny)

[SQL::Maker](http://search.cpan.org/perldoc?SQL::Maker)
