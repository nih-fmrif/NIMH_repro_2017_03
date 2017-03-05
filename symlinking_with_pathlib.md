could add a bit about symlinking with pathlib.

Best way to use symlinking is to use a relative link. That way when we transfer the files and links to another directory or system the symlinks still resolve to the appropriate files (provided we have maintained the relative locations of links and target files). 