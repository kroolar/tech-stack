### Memento

#### Opis
Behawioralny wzorzec projektowy, który pozwala na zapisywanie oraz odczytywanie stanu obiektu.

#### Problem
Chcemy stworzyć repozytorium, które będzie zapisywało nasz kod oraz pozwoli przywracać do niego dostęp.

#### Rozwiązanie
Struktura wzorca składa się z 3 klas:
- **Originator**: Zawiera logikę odpowiedzialną za zapisywanie oraz przywracanie stanów *(Repo)*
- **Memento**: Śłuży jako konkretny stan *(Commit)*
- **Caretaker**: Odpowiedzialny zapisywanie oraz przywracanie stanu. Może także śledzić historię zmian *(Project)*

``` Ruby
# Przechowuję stan oraz własne ID
class Commit
  attr_reader :id, :state

  def initialize(id:, state:)
    @id = id
    @state = state
  end
end

# Klasa odpowiedzialna za pobieranie i przywracanie stanu oraz dostęp do historii.
class Repo
  attr_reader :history, :state

  def initialize
    @state = Commit.new(id: 1, state: '')
    @history = []
  end

  def save(current_state)
    @commits << Commit.new(id: @commits.size + 1, state: current_state)
  end

  def revert(commit_id)
    commit = @commits.find { |commit| commit.id == commit_id }

    @state = commit_id
  end
end

class Project
  attr_accessor :repo, :state

  def initialize
    @state = ''
  end
end



Plus i minusy
