
# Iterator

Behavioral design pattern that allows work with aggregate object without exposing its underlaying representation. 

### Problem

We have a list of songs prepared. We want to create a class that will help us manage it, show the current song and fast forward and rewind.

``` Ruby
class MusicPlayer
  attr_reader :index, :songs

  def initialize(songs)
    @songs = songs
    @index = 0
  end
  
  def next
    song = songs[index]
    index += 1
    
    song
  end
  
  def current_song
    songs[index]
  end
  
  def has_next?
    index < songs.length
  end
  
  def previous
    song = songs[index]
    index -= 1
    
    song
  end
end
```

**Pros:**
- You can clean up the client code and the collections by extracting bulky traversal algorithms into separate classes (SRP)
- You can implement new types of collections and iterators and pass them to existing code without breaking anything (OCP)
- You can iterate over the same collection in parallel because each iterator object contains its own iteration state
- For the same reason, you can delay an iteration and continue it when needed

**Cons:**
- Applying the pattern can be an overkill if your app only works with simple collections
- Using an iterator may be less efficient than going through elements of some specialized collections directly

**Sources:**
- https://refactoring.guru/design-patterns/iterator
- https://refactoring.guru/design-patterns/iterator/ruby/example
- https://github.com/davidgf/design-patterns-in-ruby/blob/master/iterator.md
- https://medium.com/@dljerome/design-patterns-in-ruby-iterator-beead2c6492
