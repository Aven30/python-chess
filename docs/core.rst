Core
====

Colors
------

Constants for the side to move or the color of a piece.

.. py:data:: chess.WHITE
    :annotation: = True

.. py:data:: chess.BLACK
    :annotation: = False

You can get the opposite color using `not color`.

Piece types
-----------

.. py:data:: chess.NONE
    :annotation: = 0

.. py:data:: chess.PAWN
    :annotation: = 1
.. py:data:: chess.KNIGHT
    :annotation: = 2
.. py:data:: chess.BISHOP
    :annotation: = 3
.. py:data:: chess.ROOK
    :annotation: = 4
.. py:data:: chess.QUEEN
    :annotation: = 5
.. py:data:: chess.KING
    :annotation: = 6

Squares
-------

.. py:data:: chess.A1
    :annotation: = 0
.. py:data:: chess.B1
    :annotation: = 1

and so on to

.. py:data:: chess.H7
    :annotation: = 62
.. py:data:: chess.H8
    :annotation: = 63

.. py:data:: chess.SQUARES
    :annotation: = [chess.A1, chess.B1, ..., chess.G8, chess.H8]

.. py:data:: chess.SQUARE_NAMES
    :annotation: = ['a1', 'b1', ..., 'g8', 'h8']

.. py:data:: chess.FILE_NAMES
    :annotation: = ['a', 'b', ..., 'g', 'h']

.. autofunction:: chess.file_index

.. autofunction:: chess.rank_index

.. autofunction:: chess.square

Pieces
------

.. autoclass:: chess.Piece
    :members:

    .. py:attribute:: piece_type

        The piece type.

    .. py:attribute:: color

        The piece color.

Moves
-----

.. autoclass:: chess.Move
    :members:

    .. py:attribute:: from_square

        The source square.

    .. py:attribute:: to_square

        The target square.

    .. py:attribute:: promotion

        The promotion piece type.


Board
-----

.. autodata:: chess.STARTING_FEN

.. autoclass:: chess.Board
    :members:

    .. py:attribute:: turn

        The side to move.

    .. py:attribute:: castling_rights

        Bitmask of the rooks with castling rights.

        >>> white_castle_kingside = board.castling_rights & chess.BB_H1

    .. py:attribute:: ep_square

        The potential en-passant square on the third or sixth rank or `0`. It
        does not matter if en-passant would actually be possible on the next
        move.

    .. py:attribute:: fullmove_number

        Counts move pairs. Starts at `1` and is incremented after every move
        of the black side.

    .. py:attribute:: halfmove_clock

        The number of half moves since the last capture or pawn move.

    .. py:attribute:: pseudo_legal_moves
        :annotation: = PseudoLegalMoveGenerator(self)

        A dynamic list of pseudo legal moves.

        Pseudo legal moves might leave or put the king in check, but are
        otherwise valid. Null moves are not pseudo legal. Castling moves are
        only included if they are completely legal.

        For performance moves are generated on the fly and only when nescessary.
        The following operations do not just generate everything but map to
        more efficient methods.

        >>> len(board.pseudo_legal_moves)
        20

        >>> bool(board.pseudo_legal_moves)
        True

        >>> move in board.pseudo_legal_moves
        True

    .. py:attribute:: legal_moves
        :annotation: = LegalMoveGenerator(self)

        A dynamic list of completely legal moves, much like the pseudo legal
        move list.

    .. py:attribute:: move_stack

        The move stack. Use :func:`~chess.Board.push()`,
        :func:`~chess.Board.pop()` and :func:`~chess.Board.peek()` for
        manipulation.

Square sets
-----------

.. autoclass:: chess.SquareSet
    :members:

Common integer masks are:

.. py:data:: chess.BB_VOID
    :annotation: = 0
.. py:data:: chess.BB_ALL

.. py:data:: chess.BB_LIGHT_SQUARES
.. py:data:: chess.BB_DARK_SQUARES

Single squares:

.. py:data:: chess.BB_SQUARES
    :annotation: = [chess.BB_A1, chess.BB_B1, ..., chess.BB_G8, chess.BB_H8]

Ranks and files:

.. py:data:: chess.BB_RANKS
    :annotation: = [chess.BB_RANK_1, ..., chess.BB_RANK_8]

.. py:data:: chess.BB_FILES
    :annotation: = [chess.BB_FILE_A, ..., chess.BB_FILE_H]
