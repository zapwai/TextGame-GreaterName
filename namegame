#!/usr/bin/perl
#GreaterName, Copyright David Ferrone, Aug 2014
#Update 2016 (add name feature)
# # # # # # # # # # # # # # # # # #
#
# NAMEFILE is a plain text collection of names from the US census bureau.
# 
#


my $file_name = "NAMEFILE";

open (my $FILE, '<', $file_name) or die "Could not open $file_name $!";
my @names = <$FILE>; 
close $FILE;
chomp (@names);


sub is_name{
  #input: one string (a name, supposedly), IN UPPER-CASE
  #output: 1 if it's a name in the txt file, 0 otherwise
  my $input_name = $_[0];
  foreach (@names){
    if ($_ eq $input_name) {return 1;}
  }
  return 0;
}


sub insert_name{
  # Insert given name into the namefile.
  # Must be upper-case.
  # Print statement on success, or failure to open.
  
  my $input_name = $_[0];
  my $file_one=$file_name;
  
  # (It's not necessary to sort NAMEFILE, despite how it looks.)
  open (my $FILE, '>>', $file_one) or die "Failed to open $file_one for writing.\n";
  say $FILE $input_name;
  close $FILE;
  print "Success!\n";
}


sub add_name{
  print "\n\tPlease enter the name you wish to add (Q to quit to menu): ";
  chomp ( my $NameToAdd = <STDIN> );
  $NameToAdd = uc($NameToAdd);
  if (($NameToAdd eq 'Q') || ($NameToAdd eq 'QUIT')){Menu();}
  elsif (length $NameToAdd <= 1 or length $NameToAdd > 20) {print "Oh. Cute.\n\n"; Menu();}
  elsif (is_name($NameToAdd)) {print "Oh, but that is already a name!\n\n"; Menu()}
  else {print "\n\nAlright... And you are absolutely certain that $NameToAdd is a name? (type yes) ";
	chomp ( my $Response = <STDIN> );
	
	($Response eq 'yes') ? insert_name($NameToAdd) : print "Nothing was changed.\n"; 
      }   
}

sub is_gt{
  # is_gt($a, $b)
  #input: two strings, previous name and current.
  #output: 1 if current is greater than the previous, 0 otherwise.
  (my $a, my $b) = @_;
  ($a lt $b) ? return 1 : return 0;
}

sub the_game{
  # Main game loop...
  my $playing_game = 1;
  my $previous_name = "A";
  my $current_name = "A";
  my $wins = 0;
  while ($playing_game) {
    print "Enter a name: ";
    chomp ( my $input = <STDIN> );
    
    $previous_name = $current_name if (($previous_name lt $current_name)&&(is_name($current_name)));
    $current_name = uc($input);
    
    last if ($current_name eq 'QUIT');
    
    unless (!is_name($current_name)){
      if (is_gt($previous_name, $current_name)) {print "\t\tAccepted!\n"; $wins++}
      else {print "That name is not greater than the previous accepted name [$previous_name]\n"}
    } else {print "That's not a name...\n";}
  }
  
  print "Your score was $wins.\n";
  print "Thanks for playing!\n\n"; 
}


sub test_names{
  # Testing names feature, to get a feel for what works.
  print "\nEnter 'QUIT' or 'Q' to quit.\n";
  print "Enter 'MENU' or 'M' to return to the main menu.\n\n";
  print "\nEnter a name: ";
  while (<STDIN>){
    chomp;
    my $INP = uc($_);
    last if ($INP eq 'QUIT' or $INP eq 'Q');
    if ($INP eq 'MENU' or $INP eq 'M'){Menu()}
    print "\t\t", is_name($INP);
    print "\nEnter a name: ";
  }
  print "\n";
}


sub rules{
  print "\nEnter a name which follows the previous name alphabetically.\n";
  print "Enter QUIT to end the game and see your win tally.\n";
}


sub Menu{
  print "\n\n\t\t\tWelcome to Namegame!\n\n";
  print "\t (t)est names, (a)dd a name to the list,\n";
  print "See the (r)ules, (q)uit, or (p)lay! ";
  chomp (my $input_char = <STDIN>);
  if ($input_char eq 'p') {print "\n"; the_game()}
  elsif ($input_char eq 'a') {add_name()}
  elsif ($input_char eq 'r') {rules; Menu()}
  elsif ($input_char eq 't') {test_names()}
  elsif ($input_char eq 'q') {print "Be seeing you...\n";}
  else {Menu();}
}

Menu();
